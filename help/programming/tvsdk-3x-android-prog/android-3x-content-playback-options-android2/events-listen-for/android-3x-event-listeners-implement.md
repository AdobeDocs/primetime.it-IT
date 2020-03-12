---
description: I gestori di eventi consentono di rispondere agli eventi TVSDK.
seo-description: I gestori di eventi consentono di rispondere agli eventi TVSDK.
seo-title: Implementare listener e callback di eventi
title: Implementare listener e callback di eventi
uuid: f186b39e-e634-4f64-977d-279147d76c5c
translation-type: tm+mt
source-git-commit: 1034a0520590777cc0930d2f732741202bc3bc04

---


# Implementare listener e callback di eventi {#implement-event-listeners-and-callbacks}

I gestori di eventi consentono di rispondere agli eventi TVSDK.

Quando si verifica un evento, il meccanismo eventi di TVSDK chiama il gestore eventi registrato e gli trasmette le informazioni sull&#39;evento.

TVSDK definisce i listener come interfacce interne pubbliche all&#39;interno dell&#39; `MediaPlayer` interfaccia.

L&#39;applicazione deve implementare i listener di eventi per qualsiasi evento TVSDK che influisce sull&#39;applicazione.

1. Determinare gli eventi che l&#39;applicazione deve ascoltare.

   * Eventi richiesti: Ascoltare tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >Ascoltare l&#39;evento di modifica dello stato, che si verifica quando lo stato del lettore cambia in modi che è necessario conoscere. Le informazioni fornite includono errori che potrebbero influenzare le operazioni successive del lettore.

   * Per altri eventi, a seconda dell&#39;applicazione in uso, consulta Riepilogo degli eventi del lettore [Primetime](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. Implementare e aggiungere un listener di eventi per ogni evento.

   Per la maggior parte degli eventi, TVSDK trasmette argomenti ai listener di eventi. Tali valori forniscono informazioni sull&#39;evento che possono essere utili per decidere cosa fare in seguito. L&#39; `MediaPlayerEvent` enumerazione elenca tutti gli eventi che `MediaPlayer` vengono inviati. Per ulteriori informazioni, vedere [Riepilogo](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md)degli eventi del lettore Primetime.

   Ad esempio, se `mPlayer` si tratta di un&#39;istanza di `MediaPlayer`, è possibile aggiungere e strutturare un listener di eventi nel modo seguente:

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

TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.

Gli esempi seguenti mostrano l&#39;ordine di alcuni eventi che si verificano durante la riproduzione.

Quando si carica correttamente una risorsa multimediale tramite `MediaPlayer.replaceCurrentResource`, l&#39;ordine degli eventi è:

1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Caricate la risorsa multimediale sul thread principale. Se si carica una risorsa multimediale su un thread in background, questa operazione o le operazioni successive potrebbero generare un errore, ad esempio `MediaPlayerException`e uscire.

Durante la preparazione per la riproduzione tramite `MediaPlayer.prepareToPlay`, l&#39;ordine degli eventi è:

1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` se sono stati inseriti degli annunci.
1. `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARED`

Per i flussi live/lineari, durante la riproduzione con l&#39;avanzare della finestra di riproduzione e la risoluzione di ulteriori opportunità, l&#39;ordine degli eventi è:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` se sono stati inseriti degli annunci

## Ordine degli eventi pubblicitari {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando la riproduzione include la pubblicità, TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni in base agli eventi nella sequenza prevista.

Durante la riproduzione di annunci, l&#39;ordine degli eventi è:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

I seguenti eventi vengono inviati per ogni annuncio all&#39;interno dell&#39;interruzione di annuncio:

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

L&#39;esempio seguente mostra una progressione tipica degli eventi di riproduzione di annunci:

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

TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare delle azioni in risposta a questi eventi.

Per ricevere notifiche su tutti gli eventi relativi a DRM, ascolta `MediaPlayerEvent.DRM_METADATA`. TVSDK invia eventi DRM aggiuntivi attraverso la `DRMManager` classe.

## Ordine degli eventi del caricatore {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK viene inviato `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` quando si verificano eventi di caricamento.