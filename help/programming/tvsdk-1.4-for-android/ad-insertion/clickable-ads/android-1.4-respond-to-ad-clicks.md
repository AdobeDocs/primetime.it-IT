---
description: Quando un utente fa clic su un annuncio o su un pulsante correlato, l'applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.
seo-description: Quando un utente fa clic su un annuncio o su un pulsante correlato, l'applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.
seo-title: Rispondi ai clic sugli annunci
title: Rispondi ai clic sugli annunci
uuid: 31852f01-c900-48e3-ae23-7fb131c22594
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Rispondi ai clic sugli annunci{#respond-to-clicks-on-ads}

Quando un utente fa clic su un annuncio o su un pulsante correlato, l&#39;applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni relative al click-through, registrare un `AdClickedEventListener.onAdClicked`.

   Quando un utente fa clic su un annuncio o su un pulsante correlato, TVSDK invia la notifica, incluse le informazioni sulla destinazione del clic.
1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, per inviare una notifica a TVSDK, chiama `notifyClick` l’ `MediaPlayerView`.
1. Ascoltare l’ `onAdClick(AdClickEvent event)` evento da TVSDK.
1. Per recuperare l’URL click-through e le relative informazioni, utilizzate i metodi getter per l’ `AdClickEvent` istanza.
1. Metti in pausa il video.

   Per ulteriori informazioni sull’interruzione del video, consultate [Sospendere e riprendere la riproduzione.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Utilizzate le informazioni di click-through per visualizzare l&#39;URL di click-through dell&#39;annuncio e le relative informazioni.

       Ad esempio, potete visualizzare le informazioni in uno dei seguenti modi:
   
   * Nell’applicazione aprendo l’URL di click-through in un browser.

      Sulle piattaforme desktop, l’area di riproduzione dell’annuncio video viene utilizzata per richiamare gli URL di click-through ai clic dell’utente.
   * Reindirizzare gli utenti al browser Web esterno per dispositivi mobili.

      Sui dispositivi mobili, l’area di riproduzione video e video è utilizzata per altre funzioni, come nascondere e mostrare i controlli, mettere in pausa la riproduzione, espandere la visualizzazione a schermo intero e così via. Su questi dispositivi, per avviare l’URL di click-through viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsorizzazione.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riavviate la riproduzione del video.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

Ad esempio:

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
 
    } 
}; 
```

