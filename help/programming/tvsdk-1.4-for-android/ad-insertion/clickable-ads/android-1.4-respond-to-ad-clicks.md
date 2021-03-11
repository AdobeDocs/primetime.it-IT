---
description: Quando un utente fa clic su un annuncio o su un pulsante correlato, l'applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.
title: Rispondi ai clic sugli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Rispondi ai clic sugli annunci{#respond-to-clicks-on-ads}

Quando un utente fa clic su un annuncio o su un pulsante correlato, l&#39;applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni sul click-through, registrare un `AdClickedEventListener.onAdClicked`.

   Quando un utente fa clic su un annuncio o su un pulsante correlato, TVSDK invia questa notifica, incluse le informazioni sulla destinazione del clic.
1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, per inviare una notifica a TVSDK, invoca `notifyClick` sul `MediaPlayerView`.
1. Ascolta l’evento `onAdClick(AdClickEvent event)` da TVSDK.
1. Per recuperare l’URL di click-through e le relative informazioni, utilizza i metodi getter per l’istanza `AdClickEvent` .
1. Mette in pausa il video.

   Per ulteriori informazioni sull&#39;interruzione del video, vedere [Pausa e ripresa della riproduzione.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Utilizza le informazioni di click-through per visualizzare l’URL di click-through dell’annuncio e le relative informazioni.

       Ad esempio, puoi visualizzare le informazioni in uno dei seguenti modi:
   
   * Nell’applicazione aprendo l’URL di click-through in un browser.

      Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene utilizzata per richiamare URL click-through ai clic dell’utente.
   * Reindirizza gli utenti al browser web per dispositivi mobili esterno.

      Sui dispositivi mobili, l’area di riproduzione degli annunci video viene utilizzata per altre funzioni, ad esempio per nascondere e visualizzare i controlli, mettere in pausa la riproduzione, espandere a schermo intero e così via. Su questi dispositivi viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsorizzazione, per avviare l’URL di click-through.

1. Chiudi la finestra del browser in cui vengono visualizzate le informazioni relative al click-through e riprende la riproduzione del video.

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

