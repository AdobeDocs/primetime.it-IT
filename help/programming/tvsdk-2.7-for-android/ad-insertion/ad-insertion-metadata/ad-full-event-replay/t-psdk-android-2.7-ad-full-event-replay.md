---
description: La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.
seo-description: La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.
seo-title: Abilitare gli annunci nella riproduzione a tutti gli eventi
title: Abilitare gli annunci nella riproduzione a tutti gli eventi
uuid: 69244069-ef61-42e4-b2f5-62ae2561d9e1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Abilitare gli annunci nella riproduzione a tutti gli eventi {#enable-ads-in-full-event-replay-overview}

La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti presenti nel manifesto per determinare dove inserire gli annunci. Tuttavia, a volte i contenuti live/lineari possono assomigliare ai contenuti VOD. Ad esempio, al termine del contenuto live, al manifesto attivo viene aggiunto un `EXT-X-ENDLIST` tag. Per HLS, il `EXT-X-ENDLIST` tag indica che il flusso è un flusso VOD. Per inserire correttamente gli annunci, TVSDK non è in grado di distinguere automaticamente questo flusso da un flusso VOD tipico.

L’applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `AdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad Decioning non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Al contrario, specificando una diversa modalità di segnalazione, TVSDK legge tutti i cue point dal manifesto FER e va al server di annunci per ogni cue point per richiedere un&#39;interruzione annuncio. Questo processo è simile al contenuto live/DVR.

>[!TIP]
>
>Oltre a ogni richiesta associata a un cue point, TVSDK invia una richiesta aggiuntiva per annunci pre-roll.

1. Da un&#39;origine esterna, come vCMS, ottenete la modalità di segnalazione da utilizzare.
1. Create i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specificatelo `AdSignalingMode` utilizzando `AdvertisingMetadata.setSignalingMode`.

   I valori validi sono `DEFAULT`, `SERVER_MAP`, e `MANIFEST_CUES`.

   >[!IMPORTANT]
   >
   >È necessario impostare la modalità di segnalazione degli annunci prima di chiamare `prepareToPlay`. Dopo che TVSDK ha iniziato a risolvere e inserire gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Impostare la modalità quando si crea l&#39; `AuditudeSettings` oggetto.

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
