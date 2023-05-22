---
description: La riproduzione completa degli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.
title: Abilitare gli annunci nella riproduzione completa degli eventi
exl-id: 866a696d-0c5e-4665-8890-cbbaed3e7a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Abilitare gli annunci nella riproduzione completa degli eventi {#enable-ads-in-full-event-replay-overview}

La riproduzione completa degli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.

Per il contenuto live, TVSDK utilizza i metadati/suggerimenti nel manifesto per determinare dove inserire gli annunci. Tuttavia, a volte i contenuti live/lineari possono assomigliare ai contenuti VOD. Ad esempio, al termine del contenuto live, un `EXT-X-ENDLIST` viene aggiunto al manifesto live. Per HLS, `EXT-X-ENDLIST` tag significa che il flusso è un flusso VOD. Per inserire correttamente gli annunci, TVSDK non può distinguere automaticamente questo flusso da un flusso VOD tipico.

L&#39;applicazione deve comunicare a TVSDK se il contenuto è live o VOD specificando `AdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad decisioning non deve fornire l’elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Specificando invece una modalità di segnalazione diversa, TVSDK legge tutti i cue point dal manifesto FER e va all’ad server per ogni cue point per richiedere un’interruzione pubblicitaria. Questo processo è simile al contenuto live/DVR.

>[!TIP]
>
>Oltre a ogni richiesta associata a un cue point, TVSDK effettua un’ulteriore richiesta di annuncio per gli annunci pre-roll.

1. Da un&#39;origine esterna, ad esempio vCMS, ottenere la modalità di segnalazione da utilizzare.
1. Crea i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specifica `AdSignalingMode` utilizzando `AdvertisingMetadata.setSignalingMode`.

   I valori validi sono `DEFAULT`, `SERVER_MAP`, e `MANIFEST_CUES`.

   >[!IMPORTANT]
   >
   >È necessario impostare la modalità di segnalazione dell’annuncio prima di richiamare `prepareToPlay`. Una volta che TVSDK inizia a risolvere e a posizionare gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Imposta la modalità quando crei il `AuditudeSettings` oggetto.

1. Continuare la riproduzione.

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
