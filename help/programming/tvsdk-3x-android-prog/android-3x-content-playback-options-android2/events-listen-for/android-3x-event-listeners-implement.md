---
description: I gestori eventi consentono di rispondere agli eventi TVSDK.
title: Implementare listener di eventi e callback
exl-id: 1f7977e3-4f96-4c0d-ae33-319c84a33ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Implementare listener di eventi e callback  {#implement-event-listeners-and-callbacks}

I gestori eventi consentono di rispondere agli eventi TVSDK.

Quando si verifica un evento, il meccanismo degli eventi di TVSDK chiama il gestore degli eventi registrati, trasmettendogli le informazioni sull’evento.

TVSDK definisce i listener come interfacce pubbliche interne all&#39;interno del `MediaPlayer` di rete.

L&#39;applicazione deve implementare listener di eventi per tutti gli eventi TVSDK che influiscono sull&#39;applicazione.

1. Determinare gli eventi che l&#39;applicazione deve ascoltare.

   * Eventi richiesti: ascolta tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >Ascolta l’evento di modifica dello stato, che si verifica quando lo stato del lettore cambia in un modo che devi sapere. Le informazioni fornite includono errori che potrebbero influire sulle operazioni successive del lettore.

   * Per altri eventi, a seconda dell’applicazione, consulta  [Riepilogo eventi del lettore Primetime](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. Implementa e aggiungi un listener di eventi per ogni evento.

   Per la maggior parte degli eventi, TVSDK trasmette gli argomenti ai listener di eventi. Questi valori forniscono informazioni sull’evento che possono aiutarti a decidere cosa fare dopo. Il `MediaPlayerEvent` elenca tutti gli eventi che `MediaPlayer` spedizioni. Per ulteriori informazioni, consulta  [Riepilogo eventi del lettore Primetime](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   Ad esempio, se `mPlayer` è un’istanza di `MediaPlayer`, ecco come aggiungere e strutturare un listener di eventi:

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## Ordine degli eventi di riproduzione {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate sugli eventi nella sequenza prevista.

Gli esempi seguenti mostrano l’ordine di alcuni eventi che si verificano durante la riproduzione.

Quando si carica correttamente una risorsa multimediale tramite `MediaPlayer.replaceCurrentResource`, l’ordine degli eventi è:

1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Carica la risorsa multimediale sul thread principale. Se carichi una risorsa multimediale su un thread in background, questa operazione o operazioni successive potrebbero generare un errore, ad esempio `MediaPlayerException`e uscire.

Durante la preparazione per la riproduzione tramite `MediaPlayer.prepareToPlay`, l’ordine degli eventi è:

1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` se sono stati inseriti annunci.
1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARED`

Per i flussi live/lineari, durante la riproduzione man mano che la finestra di riproduzione avanza e vengono risolte opportunità aggiuntive, l’ordine degli eventi è:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` se sono stati inseriti annunci

## Ordine degli eventi pubblicitari {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando la riproduzione include annunci, TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate sugli eventi all’interno della sequenza prevista.

Durante la riproduzione degli annunci, l’ordine degli eventi è:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

I seguenti eventi vengono inviati per ogni annuncio all’interno dell’interruzione pubblicitaria:

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

L’esempio seguente mostra una progressione tipica degli eventi di riproduzione degli annunci:

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## Ordine degli eventi DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare azioni in risposta a questi eventi.

Per ricevere notifiche su tutti gli eventi relativi a DRM, attendere `MediaPlayerEvent.DRM_METADATA`. TVSDK invia ulteriori eventi DRM tramite `DRMManager` classe.

## Ordine degli eventi di caricamento {#section_5638F8EDACCE422A9425187484D39DCC}

Invii TVSDK `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` quando si verificano eventi loader.
