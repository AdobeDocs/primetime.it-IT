---
description: Il servizio di reimballaggio creativo (CRS) garantisce che un annuncio pubblicitario non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto richiama CRS quando incontra un annuncio non HLS.
seo-description: Il servizio di reimballaggio creativo (CRS) garantisce che un annuncio pubblicitario non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto richiama CRS quando incontra un annuncio non HLS.
seo-title: Panoramica del CRS
title: Panoramica del CRS
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: 4788a8de8ba47d7f448967066e1bd0fb73fdb7a8
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Panoramica di CRS {#overview-of-crs}

Il servizio di reimballaggio creativo (CRS) garantisce che un annuncio pubblicitario non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto richiama CRS quando incontra un annuncio non HLS.

>[!NOTE]
>
>Per impostazione predefinita, CRS è disabilitato. Per abilitare CRS per il tuo account, contatta il tuo responsabile tecnico  Adobe.
>
>Per informazioni sull&#39;abilitazione di CRS nelle app TVSDK, consultate l&#39;argomento *Enable CRS in TVSDK applications* (Abilitare i CRS nelle applicazioni TVSDK) nella Guida per programmatori per la vostra piattaforma. Ad esempio, per Android 3.4, consultate [Abilitare il CRS nelle applicazioni TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara gli annunci HTTP Live Streaming (HLS) e le creatività per il flusso di contenuti e inserisce pacchetti ID3 per il monitoraggio degli annunci lato client. Trascrive i file MP4, FLV e WebM ricevuti da server di annunci, reti di annunci pubblicitari e server di agenzie di terze parti in formato HLS.

Quando  Adobe Primetime e l&#39;inserimento di inserzioni incontra un annuncio non HLS creativo, lo invia al CRS per il reimballaggio, che in genere richiede non più di tre minuti. CRS invia l’annuncio transcodificato al server CDN per un utilizzo futuro. Questo si chiama **`just-in-time (JIT) repackaging`**. Potete inoltre transcodificare gli annunci pubblicitari prima che siano necessari utilizzando l&#39; [Repackage API](../../dynamic-ad-insertion/creative-repackaging-service/api-repackage.md) . Questo si chiama *`asynchronous repackaging`*.

Il responsabile tecnico dell&#39;account manager  Adobe può anche modificare alcuni comportamenti predefiniti di CRS se un altro comportamento è più adatto all&#39;applicazione. Si tratta di:

* Priorità dei formati creativi per gli annunci.

   La sezione `MediaFiles` di una risposta VAST/VMAP può contenere creativi con diversi tipi `MediaFile`. Per impostazione predefinita, il server di manifesto ne seleziona uno in base a un insieme fisso di priorità ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`).  Adobe può cambiare le priorità per il tuo account.
* Durata destinazione annuncio.

   Il server del manifesto rileva la durata dell’annuncio di destinazione dalla playlist del contenuto e lo invia a CRS.  Adobe può modificare questo comportamento in modo che CRS utilizzi sempre una durata fissa specificata per l&#39;account.
