---
description: Quando un utente fa clic su un annuncio o su un pulsante correlato, l'applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.
seo-description: Quando un utente fa clic su un annuncio o su un pulsante correlato, l'applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.
seo-title: Rispondi ai clic sugli annunci
title: Rispondi ai clic sugli annunci
uuid: abc5de2f-3ab0-4e00-908c-ea8b31387d4f
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Rispondi ai clic sugli annunci {#respond-to-clicks-on-ads}

TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.

Per TVSDK per Android, è possibile fare clic solo sugli annunci lineari.
Quando un utente fa clic su un annuncio o su un pulsante correlato, l&#39;applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni relative al click-through, registrare `AdClickedEventListener.onAdClicked`.

   Quando un utente fa clic su un annuncio o su un pulsante correlato, TVSDK invia la notifica, incluse le informazioni sulla destinazione del clic.
1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l&#39;utente tocca o fa clic sull&#39;annuncio o sul pulsante, per inviare una notifica a TVSDK, chiama `notifyClick` sull&#39; `MediaPlayerView`.
1. Ascoltare l&#39;evento `onAdClick(AdClickEvent event)` da TVSDK.
1. Per recuperare l&#39;URL click-through e le relative informazioni, utilizzate i metodi getter per l&#39;istanza `AdClickEvent`.
1. Metti in pausa il video.

   Per ulteriori informazioni sull&#39;interruzione del video, vedere [Sospendi e riprendi riproduzione](../../ad-insertion/clickable-ads/android-3x-pausing-resuming-playback.md).
1. Utilizzate le informazioni di click-through per visualizzare l&#39;URL di click-through dell&#39;annuncio e le relative informazioni. Ad esempio, potete visualizzare le informazioni in uno dei seguenti modi:

   * Nell’applicazione, aprendo l’URL di click-through in un browser.

      Sulle piattaforme desktop, l’area di riproduzione dell’annuncio video viene utilizzata per richiamare gli URL di click-through ai clic dell’utente.
   * Reindirizzare gli utenti al browser Web esterno per dispositivi mobili.

      Sui dispositivi mobili, l’area di riproduzione video e video è utilizzata per altre funzioni, come nascondere e mostrare i controlli, mettere in pausa la riproduzione, espandere la visualizzazione a schermo intero e così via. Su questi dispositivi, per avviare l’URL di click-through viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsorizzazione.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riavviate la riproduzione del video.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

Ad esempio:

```java
private AdStartedEventListener adStartedEventListener =  
  new AdStartedEventListener() { 
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
 
private AdCompletedEventListener adCompletedEventListener =  
  new AdCompletedEventListener() { 
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
 
private AdClickedEventListener adClickedEventListener =  
  new AdClickedEventListener() { 
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
