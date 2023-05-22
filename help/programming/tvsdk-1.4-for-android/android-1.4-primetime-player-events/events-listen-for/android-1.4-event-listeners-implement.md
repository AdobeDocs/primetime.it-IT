---
description: I gestori di eventi consentono a TVSDK di rispondere agli eventi.
title: Implementare listener di eventi e callback
exl-id: eda5cd4e-4ee8-4b37-a179-242e8697f61f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Implementare listener di eventi e callback{#implement-event-listeners-and-callbacks}

I gestori di eventi consentono a TVSDK di rispondere agli eventi.

Quando si verifica un evento, il meccanismo degli eventi di TVSDK chiama il gestore eventi registrato e trasmette le informazioni sull&#39;evento al gestore.

TVSDK definisce i listener come interfacce pubbliche interne nel `MediaPlayer` di rete.

L&#39;applicazione deve implementare listener di eventi per gli eventi TVSDK che influiscono sull&#39;applicazione.

Per un elenco completo degli eventi per l’analisi dei video, consulta Tracciare riproduzione video core.

1. Determina per quali eventi l&#39;applicazione deve essere in ascolto.

   * **Eventi richiesti**: ascolta tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >Evento di riproduzione `onStateChanged` fornisce lo stato del lettore, compresi gli errori. Uno qualsiasi degli stati potrebbe influire sul passaggio successivo del lettore

   * **Altri eventi**: facoltativo, a seconda dell’applicazione.

      Ad esempio, se incorpori la pubblicità nella riproduzione, implementa i callback AdPlaybackEventListener.

1. Implementa listener di eventi per ogni evento.

   TVSDK restituisce i valori dei parametri ai callback del listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire azioni appropriate.

   `MediaPlayer.EventListener` elenca tutte le interfacce di callback. Ogni interfaccia visualizza il nome del callback e i parametri restituiti per ogni evento.

   Ad esempio:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. Registrare i listener di callback con `MediaPlayer` oggetto utilizzando `MediaPlayer.addEventListener`.

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## Ordine degli eventi di riproduzione {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate sugli eventi nella sequenza prevista.

Gli esempi seguenti mostrano l’ordine di alcuni eventi che includono eventi di riproduzione.

* Quando si carica correttamente una risorsa multimediale tramite `MediaPlayer.replaceCurrentResource`, l’ordine degli eventi è:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con stato `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con stato `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Carica la risorsa multimediale sul thread principale. Se carichi una risorsa multimediale su un thread in background, questa operazione o le successive operazioni TVSDK, o entrambe, potrebbero generare un errore (ad esempio, `IllegalStateException`) e uscire.

* Durante la preparazione per la riproduzione tramite `MediaPlayer.prepareToPlay`, l’ordine degli eventi è:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` con stato `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` se sono stati inseriti annunci.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` con stato `MediaPlayerStatus.PREPARED`

* Per i flussi live/lineari, durante la riproduzione man mano che la finestra di riproduzione avanza e vengono risolte opportunità aggiuntive, l’ordine degli eventi è:

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` se sono stati inseriti annunci
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` se sono stati inseriti annunci

L’esempio seguente mostra una progressione tipica degli eventi:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## Ordine degli eventi pubblicitari {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando la riproduzione include annunci, TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate sugli eventi nella sequenza prevista.

Durante la riproduzione degli annunci, l’ordine degli eventi è:

* `AdPlaybackEventListener.onAdBreakStart`
* I seguenti vengono inviati per ogni annuncio nell’interruzione pubblicitaria:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (più volte durante la riproduzione di un annuncio)
   * `AdPlaybackEventListener.onAdClick` (per ogni clic)
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

L’esempio seguente mostra una progressione tipica degli eventi di riproduzione degli annunci:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

Durante la riproduzione degli annunci, l’ordine degli eventi è:

* `AdPlaybackEventListener.onAdBreakStart`
* I seguenti vengono inviati per ogni annuncio nell’interruzione pubblicitaria:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (più volte durante la riproduzione di un annuncio)
   * `AdPlaybackEventListener.onAdClick` (per ogni clic)
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

L’esempio seguente mostra una progressione tipica degli eventi di riproduzione degli annunci:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## Eventi QoS {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK invia eventi Quality of Service (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come ad esempio gli eventi di buffering e ricerca.

L’esempio seguente mostra una progressione tipica di questi eventi:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## Eventi DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare azioni in risposta a questi eventi.

Per ricevere notifiche su tutti gli eventi relativi a DRM, attendere `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK invia ulteriori eventi DRM tramite `DRMManager` classe.

L’esempio seguente mostra una progressione tipica:

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## Eventi del caricatore {#section_5638F8EDACCE422A9425187484D39DCC}

Il lettore può implementare azioni basate sui seguenti eventi:

| Evento | Significato |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | Caricamento delle risorse multimediali completato. |
| `onError` | Si è verificato un problema con il caricamento delle risorse multimediali. |
