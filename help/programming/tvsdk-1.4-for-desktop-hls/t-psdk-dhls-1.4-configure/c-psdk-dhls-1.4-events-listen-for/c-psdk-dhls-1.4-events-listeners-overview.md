---
description: Gli eventi da TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, ad esempio l’avvio della riproduzione di un video, o le azioni che si verificano implicitamente, ad esempio il completamento di un annuncio.
title: Ascolta gli eventi di Primetime Player
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Panoramica {#implement-event-listeners-and-callbacks-overview}

I gestori di eventi consentono a TVSDK di rispondere agli eventi. Quando si verifica un evento, il meccanismo degli eventi di TVSDK chiama il gestore eventi registrato e trasmette le informazioni sull&#39;evento al gestore.

Il runtime di Flash fornisce un meccanismo di eventi generico, che TVSDK utilizza e definisce una serie di eventi personalizzati. L&#39;applicazione deve implementare listener di eventi per gli eventi TVSDK che influiscono sull&#39;applicazione.

1. Determina per quali eventi l&#39;applicazione deve essere in ascolto.

   * **Eventi richiesti**: ascolta tutti gli eventi di riproduzione.

     >[!IMPORTANT]
     >
     >Evento di riproduzione `MediaPlayerStatusChangeEvent.STATUS_CHANGE` fornisce lo stato del lettore, compresi gli errori. Uno qualsiasi degli stati potrebbe influire sul passaggio successivo del lettore.

   * **Altri eventi**: facoltativo, a seconda dell’applicazione.

     Ad esempio, se incorpori pubblicità nella riproduzione, ascolta per tutti `AdBreakPlaybackEvent` e `AdPlaybackEvent` eventi.

1. Implementa listener di eventi per ogni evento.

   TVSDK restituisce i valori dei parametri ai callback del listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire azioni appropriate.

   Il `Event` classe elenca tutte le interfacce di callback. Ogni interfaccia visualizza i parametri restituiti per l&#39;interfaccia.

   Ad esempio:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registrare i listener di callback con `MediaPlayer` oggetto utilizzando `MediaPlayer.addEventListener`.

   `MediaPlayer` si estende `flash.events.IEventDispatcher`, che fa parte dei file core del lettore Flash e include le funzioni `addEventListener` e `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
