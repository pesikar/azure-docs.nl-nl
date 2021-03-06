---
title: Concepten van Live Events en live outputs
description: Dit onderwerp bevat een overzicht van Live Events en live outputs in Azure Media Services v3.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: conceptual
ms.date: 10/23/2020
ms.author: inhenkel
ms.openlocfilehash: 0b223fcedfdead991f7ce374f7f7814749388f90
ms.sourcegitcommit: 4e70fd4028ff44a676f698229cb6a3d555439014
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/28/2021
ms.locfileid: "98955950"
---
# <a name="live-events-and-live-outputs-in-media-services"></a>Livegebeurtenissen en live-uitvoer in Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Met Azure Media Services kunt u live gebeurtenissen aan uw klanten leveren via de Azure-Cloud. Als u uw live streaming-gebeurtenissen in Media Services v3 wilt instellen, moet u de concepten begrijpen die in dit artikel worden besproken.

> [!TIP]
> Voor klanten die migreren van Media Services v2 Api's, vervangt de **live gebeurtenis** entiteit het **kanaal** in v2 en de **Live uitvoer** vervangt het **programma**.

## <a name="live-events"></a>Livegebeurtenissen

[Live-gebeurtenissen](/rest/api/media/liveevents) zijn verantwoordelijk voor het opnemen en verwerken van live video feeds. Wanneer u een live gebeurtenis maakt, wordt er een primair en secundair invoer eindpunt gemaakt dat u kunt gebruiken om een live signaal van een extern coderings programma te verzenden. Met het externe Live coderings programma wordt de bijdrage feed naar het invoer eindpunt verzonden met behulp van het [RTMP](https://www.adobe.com/devnet/rtmp.html) -of [Smooth streaming](/openspecs/windows_protocols/ms-sstr/8383f27f-7efe-4c60-832a-387274457251) (gefragmenteerde-MP4) invoer protocol. Voor het RTMP-opname protocol kan de inhoud worden verzonden in de Clear ( `rtmp://` ) of veilig versleuteld op de kabel ( `rtmps://` ). Voor het Smooth Streaming opname protocol zijn de ondersteunde URL-schema's `http://` of `https://` .  

## <a name="live-event-types"></a>Live gebeurtenis typen

Een [live-gebeurtenis](/rest/api/media/liveevents) kan worden ingesteld op een *Pass-Through* -(een on-premises Live coderings programma verzendt een multi-bitrate stroom) of *Live encoding* (een on-premises Live Encoder verzendt een stream met één bitsnelheid). De typen worden tijdens het maken ingesteld met behulp van [LiveEventEncodingType](/rest/api/media/liveevents/create#liveeventencodingtype):

* **LiveEventEncodingType. none**: een on-premises Live coderings programma verzendt een stream met meerdere bitrates. De opgenomen stroom slaagt via de live-gebeurtenis zonder verdere verwerking. Ook wel de Pass-Through-modus genoemd.
* **LiveEventEncodingType. Standard**: een on-premises Live coderings programma verzendt een stream met één bitsnelheid naar de live-gebeurtenis en Media Services maakt meerdere bitrate-streams. Als de bijdrage-feed van 720p of hoger is, wordt met de voor instelling **Default720p** een set van 6 omzetting/bitrate-paren gecodeerd.
* **LiveEventEncodingType. Premium1080p**: een on-premises Live coderings programma verzendt een stream met één bitsnelheid naar de live-gebeurtenis en Media Services maakt meerdere bitrate-streams. De Default1080p-voor instelling bepaalt de uitvoerset van de paren Resolution/bitrates.

### <a name="pass-through"></a>Pass-through

![Pass-through live-gebeurtenis met Media Services voorbeeld diagram](./media/live-streaming/pass-through.svg)

Wanneer u de gebeurtenis Pass-Through **Live** gebruikt, vertrouwt u met uw on-premises Live coderings programma om een video stroom met meerdere bitsnelheden te genereren en deze te verzenden als de bijdrage aan de live-gebeurtenis (met RTMP-of gefragmenteerd-MP4-Protocol). De live-gebeurtenis voert vervolgens de binnenkomende video-streams uit zonder verdere verwerking. Een dergelijke door gang werkende gebeurtenis is geoptimaliseerd voor langlopende Live-gebeurtenissen of 24x365e lineaire live-streaming. Als u dit type live gebeurtenis maakt, geeft u geen op (LiveEventEncodingType. none).

U kunt de bijdragefeed verzenden bij een resolutie tot maximaal 4K en een framesnelheid van 60 frames per seconde, met ofwel H.264/AVC- of H.265/HEVC-videocodecs, en AAC (AAC-LC, HE-AACv1 of HE-AACv2)-audiocodec. Zie vergelijking van live- [gebeurtenis typen](live-event-types-comparison.md)voor meer informatie.

> [!NOTE]
> Het gebruik van een Pass-Through-methode is de meest rendabele manier om live streamen uit te voeren wanneer u meerdere gebeurtenissen gedurende een lange periode uitvoert, en u hebt al geïnvesteerd in on-premises encoders. Zie de [prijs](https://azure.microsoft.com/pricing/details/media-services/) informatie.
>

Zie een .NET-code voorbeeld in [MediaV3LiveApp](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/blob/master/NETCore/Live/MediaV3LiveApp/Program.cs#L126).

### <a name="live-encoding"></a>Live Encoding  

![voorbeeld diagram van Live encoding met Media Services](./media/live-streaming/live-encoding.svg)

Wanneer u live encoding met Media Services gebruikt, configureert u uw on-premises Live coderings programma voor het verzenden van een video met één bitsnelheid als de invoer van de bijdrage aan de live-gebeurtenis (met RTMP-of Fragmented-Mp4-Protocol). Vervolgens stelt u een live gebeurtenis in, zodat deze de inkomende single-bitrate stroom naar een [video stroom met meerdere bitsnelheden](https://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)codeert en de uitvoer beschikbaar maakt voor het afspelen van apparaten via protocollen zoals MPEG-Dash, HLS en Smooth streaming.

Wanneer u gebruikmaakt van Live encoding, kunt u de invoer van de bijdrage alleen verzenden naar oplossingen tot 1080p-resolutie met een frame snelheid van 30 frames per seconde, met H. 264/AVC Video codec en AAC (AAC-LC, HE-AACv1 of AACv2) audiocodec. Houd er rekening mee dat door gegeven Live-gebeurtenissen oplossingen kunnen ondersteunen van Maxi maal 4.000 tot 60 frames per seconde. Zie vergelijking van live- [gebeurtenis typen](live-event-types-comparison.md)voor meer informatie.

De resoluties en bitrates die zijn opgenomen in de uitvoer van het Live coderings programma, worden bepaald door de voor instelling. Als u gebruikmaakt van een **standaard** Live coderings programma (LiveEventEncodingType. Standard), geeft de *Default720p* -voor instelling een set van zes omzettings/bitsnelheid-paren aan, van 720p tot 3,5 Mbps omlaag tot 192p bij 200 kbps. Als u een **Premium1080p** Live coderings programma (LiveEventEncodingType. Premium1080p) gebruikt, wordt met de voor instelling voor *Default1080p* een set van zes omzettings-en frequentie paren opgegeven, van 1080p tot 3,5 Mbps omlaag tot 180p met 200 kbps. Zie [Systeemwaarden](live-event-types-comparison.md#system-presets) voor meer informatie.

> [!NOTE]
> Als u de voor instelling voor Live encoding wilt aanpassen, opent u een ondersteunings ticket via Azure Portal. Geef de gewenste tabel met omzetting en bitsnelheden op. Controleer of er slechts één laag is op 720p (als u een voor instelling voor een Standard-coderings programma aanvraagt) of op 1080p (als u een voor instelling voor een Premium1080p Live Encoder wilt aanvragen) en 6 lagen.

## <a name="creating-live-events"></a>Live-gebeurtenissen maken

### <a name="options"></a>Opties

Wanneer u een live gebeurtenis maakt, kunt u de volgende opties opgeven:

* U kunt de live-gebeurtenis een naam en een beschrijving geven.
* Cloud encoding bevat Pass-Through (geen Cloud codering), standaard (tot 720p) of Premium (Maxi maal 1080p). Voor de standaard-en Premium-code ring kunt u de stretch-modus van de gecodeerde video kiezen.
  * Geen: de uitvoer resolutie die is opgegeven in de voor instelling voor de code ring wordt strikt gezien zonder rekening te houden met de hoogte-breedte verhouding pixel of de hoogte-breedte verhouding van de invoer video.
  * AutoSize: overschrijft de uitvoer resolutie en wijzigt deze zodat deze overeenkomt met de weergave hoogte-breedte verhouding van de invoer, zonder opvulling. Als de invoer bijvoorbeeld 1920 is en de voor instelling voor code ring vraagt om 1280x1280, wordt de waarde in de voor instelling overschreven en wordt de uitvoer op 1280x720, die de invoer hoogte-breedte verhouding van 16:9 bijhoudt.
  * AutoAanpassen: Hiermee wordt de uitvoer (met een letterbox of een pijler) om de uitvoer resolutie te voldoen, en wordt ervoor gezorgd dat de actieve video regio in de uitvoer dezelfde hoogte-breedte verhouding heeft als de invoer. Als de invoer bijvoorbeeld 1920 is en de voor instelling voor code ring vraagt om 1280x1280, is de uitvoer op 1280x1280, die een binnenste rechthoek bevat van 1280x720 met een hoogte-breedte verhouding van 16:9, met de regio's van de pijler 280 pixels breed aan de linkerkant en de rechter kant.
* Streaming-Protocol (momenteel worden de protocollen RTMP en Smooth Streaming ondersteund). U kunt de protocol optie niet wijzigen terwijl de live-gebeurtenis of de eraan gekoppelde actieve uitvoer bewerkingen worden uitgevoerd. Als u verschillende protocollen nodig hebt, maakt u een afzonderlijke live-gebeurtenis voor elk streaming-protocol.
* Invoer-ID die een Globally Unique Identifier is voor de invoer stroom van de live-gebeurtenis.
* Statisch hostname-voor voegsel dat geen bevat (in dat geval wordt een wille keurige 128-bits hexadecimale teken reeks gebruikt), de naam van een live-gebeurtenis gebruiken of een aangepaste naam gebruiken.  Wanneer u ervoor kiest om de naam van een klant te gebruiken, is deze waarde het voor voegsel van de aangepaste hostnaam.
* U kunt de end-to-end latentie tussen de live-uitzending en het afspelen verminderen door het interval voor de invoer sleutel frames in te stellen, de duur (in seconden) van elk media segment in de HLS-uitvoer. De waarde moet een geheel getal zijn dat niet gelijk is aan nul in het bereik van 0,5 tot 20 seconden.  De standaard waarde is 2 seconden als *geen* van de invoer-of uitvoer sleutel kader intervallen zijn ingesteld. Het interval voor sleutel frames is alleen toegestaan voor Pass-Through-gebeurtenissen.
* Wanneer u de gebeurtenis maakt, kunt u deze instellen op automatisch starten. Wanneer auto start is ingesteld op True, wordt de live-gebeurtenis gestart nadat deze is gemaakt. De facturering begint zodra de live-gebeurtenis wordt gestart. U moet stoppen op de resource van de live-gebeurtenis expliciet aanroepen om verdere facturering te stoppen. U kunt ook de gebeurtenis starten wanneer u klaar bent om te streamen.

> [!NOTE]
> De maximale frame snelheid is 30 fps voor de standaard-en Premium-code ring.

## <a name="standby-mode"></a>Modus stand-by

Wanneer u een live gebeurtenis maakt, kunt u deze instellen op de modus stand-by. De gebeurtenis bevindt zich in de modus stand-by, maar u kunt de beschrijving, het voor voegsel van de statische hostnaam en de toegangs instellingen voor invoer en voor beeld beperken.  De modus stand-by is nog steeds een factureer bare modus, maar heeft een andere prijs dan wanneer u een live stream Start.

Zie [Live Event States and billing](live-event-states-billing.md)(Engelstalig) voor meer informatie.

* IP-beperkingen voor de opname en voorbeeldweergave. U kunt de IP-adressen definiëren die een video mogen opnemen in deze live-gebeurtenis. Toegestane IP-adressen kunnen worden opgegeven als één IP-adres (bijvoorbeeld 10.0.0.1), een IP-adresbereik met een IP-adres en een CIDR-subnetmasker (bijvoorbeeld 10.0.0.1/22) of een IP-adresbereik met een IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld , ' 10.0.0.1(255.255.252.0)').
<br/><br/>
Als geen IP-adressen zijn opgegeven en er geen regeldefinitie bestaat, zijn er geen IP-adressen toegestaan. Als u IP-adres(sen) wilt toestaan, maakt u een regel en stelt u 0.0.0.0/0 in.<br/>De IP-adressen moeten een van de volgende indelingen hebben: IpV4-adres met 4 cijfers of een CIDR-adresbereik.
<br/><br/>
Als u bepaalde Ip's wilt inschakelen op uw eigen firewalls of als u invoer wilt beperken voor uw Live-gebeurtenissen in azure IP-adressen, downloadt u een JSON-bestand van de IP-adresbereiken van het [Azure-Data Center](https://www.microsoft.com/download/details.aspx?id=41653). Selecteer de sectie **Details** op de pagina voor meer informatie over dit bestand.

* Wanneer u de gebeurtenis maakt, kunt u ervoor kiezen om live-transcripties in te scha kelen. Live transcriptie is standaard uitgeschakeld. Voor meer informatie over Live transcriptie Read [Live transcriptie](live-transcription.md).

### <a name="naming-rules"></a>Naamgevingsregels

* De maximale naam van een live-gebeurtenis is 32 tekens.
* De naam moet volgen op dit [regex](/dotnet/standard/base-types/regular-expression-language-quick-reference) -patroon: `^[a-zA-Z0-9]+(-*[a-zA-Z0-9])*$` .

Zie ook [naam conventies voor streaming-eind punten](streaming-endpoint-concept.md#naming-convention).

> [!TIP]
> Als u de unieke naam van uw live-evenement wilt waarborgen, kunt u een GUID genereren en vervolgens alle afbreek streepjes en accolades verwijderen (indien van toepassing). De teken reeks is uniek voor alle Live-gebeurtenissen en de lengte ervan is gegarandeerd 32.

## <a name="live-event-ingest-urls"></a>Url's voor Live Event opname

Zodra de live gebeurtenis is gemaakt, kunt u opname-Url's ophalen die u aanbiedt aan de Live on-premises encoder. De live-encoder gebruikt deze URL's voor het invoeren van een live-stream. Zie [Aanbevolen on-premises Live coderings](recommended-on-premises-live-encoders.md)Programma's voor meer informatie.

>[!NOTE]
> Vanaf de 2020-05-01 API-release worden Vanity Url's aangeduid als statische hostnamen

U kunt niet-vanity-URL's en vanity-URL's gebruiken.

> [!NOTE]
> Stel de vanity-modus in om een URL voor opnemen voorspellend te maken.

* Niet-Vanity-URL

    Niet-Vanity-URL is de standaard modus in Media Services v3. Mogelijk wordt de live-gebeurtenis snel opgehaald, maar is de opname-URL alleen bekend wanneer de live-gebeurtenis wordt gestart. Als u de live-gebeurtenis stopt/start, wordt de URL gewijzigd. Niet-Vanity is handig in scenario's wanneer een eind gebruiker wil streamen met behulp van een app waarin de app een live gebeurtenis spoed wil ontvangen en een dynamische opname-URL geen problemen vormt.

    Als een client-app geen opname-URL hoeft te genereren voordat de live-gebeurtenis wordt gemaakt, kunt u Media Services automatisch het toegangs token genereren voor de live-gebeurtenis.

* Vanity-URL

    De Vanity-modus wordt aanbevolen door grote media-broadcasters die gebruikmaken van hardware broadcast encoders en ze hun encoders niet opnieuw moeten configureren wanneer ze de live-gebeurtenis starten. Deze broadcasters willen een voorspellende opname-URL die in de loop van de tijd niet verandert.

    > [!NOTE]
    > In de Azure Portal heeft de Vanity-URL de naam '*statisch hostname-voor voegsel*'.

    Als u deze modus in de API wilt opgeven, moet u instellen op de `useStaticHostName` `true` aanmaak tijd (standaard instelling `false` ). Wanneer `useStaticHostname` is ingesteld op True, `hostnamePrefix` geeft het het eerste deel van de hostnaam aan die is toegewezen aan de preview van Live Event en opname-eind punten. De uiteindelijke hostnaam zou een combi natie zijn van dit voor voegsel, de naam van het media service account en een korte code voor het Azure Media Services Data Center.

    Als u een wille keurig token in de URL wilt vermijden, moet u ook uw eigen toegangs token () door geven `LiveEventInput.accessToken` tijdens de aanmaak tijd.  Het toegangs token moet een geldige GUID-teken reeks zijn (met of zonder de afbreek streepjes). Zodra de modus is ingesteld, kan deze niet worden bijgewerkt.

    Het toegangs token moet uniek zijn in uw Data Center. Als uw app een Vanity-URL moet gebruiken, is het raadzaam om altijd een nieuw GUID-exemplaar voor uw toegangs token te maken (in plaats van een bestaande GUID opnieuw te gebruiken).

    Gebruik de volgende Api's om de Vanity-URL in te scha kelen en het toegangs token in te stellen op een geldige GUID (bijvoorbeeld `"accessToken": "1fce2e4b-fb15-4718-8adc-68c6eb4c26a7"` ).  

    |Taal|Vanity-URL inschakelen|Toegangstoken instellen|
    |---|---|---|
    |REST|[Eigenschappen. vanityUrl](/rest/api/media/liveevents/create#liveevent)|[LiveEventInput. accessToken](/rest/api/media/liveevents/create#liveeventinput)|
    |CLI|[--Vanity-URL](/cli/azure/ams/live-event?view=azure-cli-latest#az-ams-live-event-create)|[--Access-token](/cli/azure/ams/live-event?view=azure-cli-latest#optional-parameters)|
    |.NET|[LiveEvent.VanityUrl](/dotnet/api/microsoft.azure.management.media.models.liveevent?view=azure-dotnet#Microsoft_Azure_Management_Media_Models_LiveEvent_VanityUrl)|[LiveEventInput. AccessToken](/dotnet/api/microsoft.azure.management.media.models.liveeventinput.accesstoken?view=azure-dotnet#Microsoft_Azure_Management_Media_Models_LiveEventInput_AccessToken)|

### <a name="live-ingest-url-naming-rules"></a>Naamgevingsregels voor live-opname-URL's

* De *willekeurige* tekenreeks hieronder is een 128-bits hexadecimaal getal (bestaande uit 32 tekens, van 0-9 en a-f).
* *uw toegangs token*: de geldige GUID-teken reeks die u instelt wanneer u de Vanity-modus gebruikt. Bijvoorbeeld `"1fce2e4b-fb15-4718-8adc-68c6eb4c26a7"`.
* *Stream name*: geeft de naam van de stream voor een specifieke verbinding aan. De waarde van de stroom naam wordt meestal toegevoegd door de live encoder die u gebruikt. U kunt het Live coderings programma zodanig configureren dat elke naam wordt gebruikt om de verbinding te beschrijven, bijvoorbeeld: "video1_audio1", "video2_audio1", "Stream".

#### <a name="non-vanity-url"></a>Niet-Vanity-URL

##### <a name="rtmp"></a>RTMP

`rtmp://<random 128bit hex string>.channel.media.azure.net:1935/live/<auto-generated access token>/<stream name>`<br/>
`rtmp://<random 128bit hex string>.channel.media.azure.net:1936/live/<auto-generated access token>/<stream name>`<br/>
`rtmps://<random 128bit hex string>.channel.media.azure.net:2935/live/<auto-generated access token>/<stream name>`<br/>
`rtmps://<random 128bit hex string>.channel.media.azure.net:2936/live/<auto-generated access token>/<stream name>`<br/>

##### <a name="smooth-streaming"></a>Vloeiend streamen

`http://<random 128bit hex string>.channel.media.azure.net/<auto-generated access token>/ingest.isml/streams(<stream name>)`<br/>
`https://<random 128bit hex string>.channel.media.azure.net/<auto-generated access token>/ingest.isml/streams(<stream name>)`<br/>

#### <a name="vanity-url"></a>Vanity-URL

In de volgende paden `<live-event-name>` staat voor de naam van de gebeurtenis of de aangepaste naam die wordt gebruikt bij het maken van de live-gebeurtenis.

##### <a name="rtmp"></a>RTMP

`rtmp://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:1935/live/<your access token>/<stream name>`<br/>
`rtmp://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:1936/live/<your access token>/<stream name>`<br/>
`rtmps://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:2935/live/<your access token>/<stream name>`<br/>
`rtmps://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:2936/live/<your access token>/<stream name>`<br/>

##### <a name="smooth-streaming"></a>Vloeiend streamen

`http://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net/<your access token>/ingest.isml/streams(<stream name>)`<br/>
`https://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net/<your access token>/ingest.isml/streams(<stream name>)`<br/>

## <a name="live-event-preview-url"></a>Preview-URL voor Live Event

Zodra de live-gebeurtenis begint met het ontvangen van de contributie, kunt u het preview-eind punt gebruiken om te bekijken en te controleren of u de Live Stream ontvangt voordat u verder gaat publiceren. Nadat u hebt gecontroleerd of de voorbeeld stroom goed is, kunt u de live-gebeurtenis gebruiken om de live-stream beschikbaar te maken voor levering via een of meer (vooraf gemaakte) streaming-eind punten. U kunt dit doen door een nieuwe [Live-uitvoer](/rest/api/media/liveoutputs) te maken voor de live-gebeurtenis.

> [!IMPORTANT]
> Zorg ervoor dat de video stroomt naar de Preview-URL voordat u doorgaat.

## <a name="live-event-long-running-operations"></a>Langlopende bewerkingen voor Live Event

Zie [langlopende bewerkingen](media-services-apis-overview.md#long-running-operations)voor meer informatie.

## <a name="live-outputs"></a>Live uitvoer

Zodra u de stroom naar de live gebeurtenis hebt gestroomd, kunt u de streaming-gebeurtenis starten door een [Asset](/rest/api/media/assets), [Live output](/rest/api/media/liveoutputs)en [streaming-Locator](/rest/api/media/streaminglocators)te maken. Live uitvoer archiveert de stream en maakt deze beschikbaar voor gebruikers via het [streaming-eind punt](/rest/api/media/streamingendpoints).  

Zie [een Cloud-DVR gebruiken](live-event-cloud-dvr.md)voor meer informatie over live-uitvoer.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

Zie het artikel [Veelgestelde vragen](frequently-asked-questions.md#live-streaming) .

## <a name="ask-questions-and-get-updates"></a>Vragen stellen en updates ophalen

Ga naar het artikel van de [Azure Media Services-community](media-services-community.md) voor verschillende manieren om vragen te stellen, feedback te geven en updates voor Media Services op te halen.

## <a name="next-steps"></a>Volgende stappen

[Zelf studie over live streamen](stream-live-tutorial-with-api.md)
