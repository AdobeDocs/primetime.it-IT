---
description: Il CRS (creative repackaging service) garantisce che un annuncio non HLS e un creativo possano essere riprodotti correttamente nei flussi HLS. Il server manifesto chiama su CRS quando incontra un annuncio non HLS.
title: Panoramica del CRS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Panoramica di CRS {#overview-of-crs}

Il CRS (creative repackaging service) garantisce che un annuncio non HLS e un creativo possano essere riprodotti correttamente nei flussi HLS. Il server manifesto chiama su CRS quando incontra un annuncio non HLS.

>[!NOTE]
>
>Per impostazione predefinita, CRS è disabilitato. Per abilitare CRS per il tuo account, contatta il tuo Adobe technical account manager.
>
>Per informazioni sull&#39;abilitazione di CRS nelle app TVSDK, consulta l&#39;argomento *Abilita CRS nelle applicazioni TVSDK* nella Guida per il programmatore della piattaforma. Ad esempio, per Android 3.4, consulta [Abilitare CRS nelle applicazioni TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara HTTP Live Streaming (HLS) e crea contenuti per il flusso di contenuti e inserisce pacchetti ID3 per il tracciamento degli annunci lato client. Trascodifica i file MP4, FLV e WebM ricevuti da server di annunci di terze parti, reti di annunci e server di agenzie in formato HLS.

Quando l&#39;inserimento di annunci Adobe Primetime incontra un annuncio non HLS creativo, lo invia a CRS per il riconfezionamento, che in genere richiede non più di tre minuti. CRS invia l’annuncio transcodificato al server CDN per un utilizzo futuro. Questo si chiama **`just-in-time (JIT) repackaging`**. Puoi anche transcodificare le creatività degli annunci prima che siano necessarie utilizzando l&#39; [API di ricompilazione](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Questo si chiama *`asynchronous repackaging`*.

Il tuo Adobe Technical account manager può anche modificare alcuni comportamenti predefiniti di CRS se un altro comportamento è più adatto alla tua applicazione. Si tratta di:

* Priorità dei formati creativi degli annunci.

   La sezione `MediaFiles` di una risposta VAST/VMAP può contenere creativi con diversi tipi `MediaFile`. Per impostazione predefinita, il server manifest ne seleziona uno in base a un set fisso di priorità ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe può modificare le priorità del tuo account.
* Durata dell&#39;annuncio.

   Il server manifest rileva la durata dell&#39;annuncio target dalla playlist del contenuto e lo invia a CRS. Adobe può modificare questo comportamento in modo che CRS utilizzi sempre una durata fissa specificata per il tuo account.
