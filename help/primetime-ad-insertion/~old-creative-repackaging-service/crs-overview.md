---
description: Il servizio di repackaging creativo (CRS) garantisce che un materiale creativo e non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto effettua una chiamata a CRS quando rileva un annuncio non HLS.
title: Panoramica di CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Panoramica di CRS {#overview-of-crs}

Il servizio di repackaging creativo (CRS) garantisce che un materiale creativo e non HLS possa essere riprodotto correttamente nei flussi HLS. Il server manifesto effettua una chiamata a CRS quando rileva un annuncio non HLS.

>[!NOTE]
>
>Per impostazione predefinita, CRS è disabilitato. Per abilitare CRS per il tuo account, contatta il tuo account manager tecnico di Adobe.
>
>Per informazioni sull&#39;abilitazione di CRS nelle app TVSDK, vedi *Abilitare CRS nelle applicazioni TVSDK* nella Guida per programmatori della piattaforma. Ad esempio, per Android 3.4, consulta [Abilitare CRS nelle applicazioni TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepara le creatività degli annunci HTTP Live Streaming (HLS) per il flusso di contenuti e inserisce pacchetti ID3 per il tracciamento degli annunci lato client. Converte in formato HLS i file MP4, FLV e WebM ricevuti da server di annunci di terze parti, reti di annunci e server di agenzie.

Quando Adobe Primetime ad insertion rileva un annuncio non HLS, lo invia a CRS per il repackaging, che in genere richiede non più di tre minuti. CRS invia l’annuncio transcodificato e creativo al server CDN per un utilizzo futuro. Questo è chiamato **`just-in-time (JIT) repackaging`**. Puoi anche transcodificare i contenuti pubblicitari prima che siano necessari utilizzando  [Riconfezionamento API](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Questo è chiamato *`asynchronous repackaging`*.

Il tuo account manager tecnico Adobe può anche modificare alcuni comportamenti predefiniti di CRS se un altro comportamento è più adatto alla tua applicazione. Si tratta dei seguenti:

* Priorità dei formati pubblicitari.

   Il `MediaFiles` sezione di una risposta VAST/VMAP può contenere creativi con diversi `MediaFile` tipi. Per impostazione predefinita, il server manifest ne seleziona una in base a un insieme di priorità fisse ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe può modificare le priorità per il tuo account.
* Durata dell’annuncio target.

   Il server manifest rileva la durata dell’annuncio di destinazione dalla playlist dei contenuti e la invia a CRS. Adobe può modificare questo comportamento in modo che CRS utilizzi sempre una durata fissa specificata per il tuo account.
