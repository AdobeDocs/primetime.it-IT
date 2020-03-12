---
description: Il servizio di reimballaggio creativo (CRS) garantisce che un annuncio pubblicitario non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto richiama CRS quando incontra un annuncio non HLS.
seo-description: Il servizio di reimballaggio creativo (CRS) garantisce che un annuncio pubblicitario non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto richiama CRS quando incontra un annuncio non HLS.
seo-title: Panoramica del CRS
title: Panoramica del CRS
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: 4788a8de8ba47d7f448967066e1bd0fb73fdb7a8

---


# Panoramica del CRS {#overview-of-crs}

Il servizio di reimballaggio creativo (CRS) garantisce che un annuncio pubblicitario non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto richiama CRS quando incontra un annuncio non HLS.

>[!NOTE]
>
>Per impostazione predefinita, CRS è disabilitato. Per abilitare CRS per il tuo account, contatta il tuo responsabile tecnico Adobe.
>
>Per informazioni sull&#39;abilitazione di CRS nelle app TVSDK, consultate l&#39;argomento *Abilitare CRS nelle applicazioni* TVSDK nella Guida per programmatori per la vostra piattaforma. Ad esempio, per Android 3.4, consultate [Abilitare i CRS nelle applicazioni TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara gli annunci HTTP Live Streaming (HLS) e le creatività per il flusso di contenuti e inserisce pacchetti ID3 per il monitoraggio degli annunci lato client. Trascrive i file MP4, FLV e WebM ricevuti da server di annunci, reti di annunci pubblicitari e server di agenzie di terze parti in formato HLS.

Quando Adobe Primetime ad inserzione incontra un annuncio pubblicitario non HLS, lo invia a CRS per il reimballaggio, che in genere richiede non più di tre minuti. CRS invia l’annuncio transcodificato al server CDN per un utilizzo futuro. Questo si chiama **`just-in-time (JIT) repackaging`**. Potete inoltre transcodificare gli annunci pubblicitari prima che siano necessari tramite l&#39;API [](../../dynamic-ad-insertion/creative-repackaging-service/api-repackage.md) Repackage. Questo si chiama *`asynchronous repackaging`*.

Il vostro account manager tecnico Adobe può anche modificare alcuni comportamenti predefiniti di CRS se un altro comportamento è più adatto all&#39;applicazione. Si tratta di:

* Priorità dei formati creativi per gli annunci.

   La `MediaFiles` sezione di una risposta VAST/VMAP può contenere creativi con diversi `MediaFile` tipi. Per impostazione predefinita, il server manifesto ne seleziona uno in base a un insieme fisso di priorità ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe può cambiare le priorità del tuo account.
* Durata destinazione annuncio.

   Il server del manifesto rileva la durata dell’annuncio di destinazione dalla playlist del contenuto e lo invia a CRS. Adobe può modificare questo comportamento in modo che CRS utilizzi sempre una durata fissa specificata per l&#39;account.
