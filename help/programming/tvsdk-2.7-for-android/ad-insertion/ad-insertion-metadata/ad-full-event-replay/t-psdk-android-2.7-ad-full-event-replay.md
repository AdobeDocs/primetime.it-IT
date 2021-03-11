---
description: La riproduzione a eventi completi (FER) è una risorsa VOD che agisce come risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci siano posizionati correttamente.
title: Abilitare gli annunci nella riproduzione completa degli eventi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Abilitare gli annunci nella riproduzione completa degli eventi {#enable-ads-in-full-event-replay-overview}

La riproduzione a eventi completi (FER) è una risorsa VOD che agisce come risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci siano posizionati correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti nel manifesto per determinare dove collocare gli annunci. Tuttavia, a volte i contenuti live/lineari potrebbero assomigliare al contenuto VOD. Ad esempio, al completamento del contenuto live, al manifesto live viene aggiunto un tag `EXT-X-ENDLIST` . Per HLS, il tag `EXT-X-ENDLIST` indica che il flusso è un flusso VOD. Per inserire correttamente gli annunci, TVSDK non può distinguere automaticamente questo flusso da un flusso VOD tipico.

L’applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `AdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad decisioning non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Invece, specificando una modalità di segnalazione diversa, TVSDK legge tutti i punti di cue dal manifesto FER e va al server di annunci per ogni punto di cue per richiedere un&#39;interruzione pubblicitaria. Questo processo è simile al contenuto live/DVR.

>[!TIP]
>
>Oltre a ogni richiesta associata a un punto di cue, TVSDK invia una richiesta aggiuntiva di annunci per annunci pre-roll.

1. Da un&#39;origine esterna, ad esempio vCMS, ottenere la modalità di segnalazione da utilizzare.
1. Crea i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specifica `AdSignalingMode` utilizzando `AdvertisingMetadata.setSignalingMode`.

   I valori validi sono `DEFAULT`, `SERVER_MAP` e `MANIFEST_CUES`.

   >[!IMPORTANT]
   >
   >È necessario impostare la modalità di segnalazione degli annunci prima di chiamare `prepareToPlay`. Dopo che TVSDK inizia a risolvere e posizionare gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Impostare la modalità quando si crea l&#39;oggetto `AuditudeSettings` .

1. Continua a riprodurre.

<!--<a id="example_6DECA71C3C3B4551805C09A80686552F"></a>-->

```java
MediaPlayer mediaPlayer =  
  new MediaPlayer(getActivity.().getApplicationContext()); 
 
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings.setSignalingMode(AdSignalingMode.MANIFEST_CUES); 
auditudeSettings.setDomain("your-auditude-domain"); 
auditudeSettings.setZoneId("your-auditude-zone-id"); 
auditudeSettings.setMediaId("your-media-id"); 
// set additional targeting parameters or custom parameters 
 
MediaPlayerItemConfig itemConfig =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
MediaResource mediaResource =  
  new MediaResource("https://example.com/media/test_media.m3u8",  
                    MediaResource.Type.HLS, Metadata); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
            // TVSDK is in the PREPARED state, so start the playback 
            mediaPlayer.play(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.COMPLETE ) { 
            // playback has reached the end of stream ( ads included ) 
            // if we want to rewind we can call 
            mediaPlayer.seek(mediaPlayer.getSeekableRange().getBegin()); 
        } 
    } 
}); 
 
mediaPlayer.replaceCurrentResource(mediaResource, itemConfig); 
```
