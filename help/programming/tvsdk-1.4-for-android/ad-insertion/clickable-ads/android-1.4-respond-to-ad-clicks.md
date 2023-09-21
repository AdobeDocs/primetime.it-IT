---
description: Quando un utente fa clic su un annuncio o su un pulsante correlato, l’applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione del clic.
title: Rispondi ai clic sugli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Rispondi ai clic sugli annunci{#respond-to-clicks-on-ads}

Quando un utente fa clic su un annuncio o su un pulsante correlato, l’applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione del clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni di click-through, registrare un `AdClickedEventListener.onAdClicked`.

   Quando un utente fa clic su un annuncio o su un pulsante correlato, TVSDK invia questa notifica, incluse informazioni sulla destinazione del clic.
1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, per notificare TVSDK, chiama `notifyClick` il `MediaPlayerView`.
1. Ascolta la `onAdClick(AdClickEvent event)` da TVSDK.
1. Per recuperare l’URL di click-through e le informazioni correlate, utilizza i metodi getter per `AdClickEvent` dell&#39;istanza.
1. Metti in pausa il video.

   Per ulteriori informazioni sulla sospensione del video, consulta [Sospendi e riprendi la riproduzione.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Utilizza le informazioni di click-through per visualizzare l’URL di click-through dell’annuncio e le relative informazioni.

       Ad esempio, puoi visualizzare le informazioni in uno dei seguenti modi:
   
   * Nell’applicazione aprendo l’URL di click-through in un browser.

     Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene utilizzata per richiamare gli URL di click-through ai clic dell’utente.
   * Reindirizza gli utenti al browser Web mobile esterno.

     Sui dispositivi mobili, l’area di riproduzione e il video vengono utilizzati per altre funzioni, ad esempio per nascondere e visualizzare i controlli, mettere in pausa la riproduzione, espandersi a schermo intero e così via. Su questi dispositivi, per avviare l’URL di click-through viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsor.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riprendete la riproduzione del video.

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
