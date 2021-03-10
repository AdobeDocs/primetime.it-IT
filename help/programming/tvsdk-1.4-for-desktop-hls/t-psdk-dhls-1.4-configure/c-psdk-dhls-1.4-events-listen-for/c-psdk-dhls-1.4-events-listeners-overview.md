---
description: Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, ad esempio un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, ad esempio il completamento di un annuncio.
title: Ascolta gli eventi di Primetime Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Panoramica {#implement-event-listeners-and-callbacks-overview}

I gestori di eventi consentono a TVSDK di rispondere agli eventi. Quando si verifica un evento, il meccanismo eventi di TVSDK chiama il gestore eventi registrato e trasmette le informazioni sull&#39;evento al gestore.

Flash Runtime fornisce un meccanismo di eventi generici, che TVSDK utilizza e definisce una serie di eventi personalizzati. L’applicazione deve implementare listener di eventi per gli eventi TVSDK che influiscono sull’applicazione.

Per un elenco completo degli eventi per l&#39;analisi video, consulta [Tracciare la riproduzione di video core](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html).

1. Determinare gli eventi che l&#39;applicazione deve ascoltare.

   * **Eventi** richiesti: Ascoltare tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >L&#39;evento di riproduzione `MediaPlayerStatusChangeEvent.STATUS_CHANGE` fornisce lo stato del lettore, compresi gli errori. Uno qualsiasi degli stati potrebbe influenzare il passaggio successivo del lettore.

   * **Altri eventi**: Facoltativo, a seconda dell’applicazione.

      Ad esempio, se incorpori pubblicità nella riproduzione, ascolta tutti gli eventi `AdBreakPlaybackEvent` e `AdPlaybackEvent`.

1. Implementa i listener di eventi per ogni evento.

   TVSDK restituisce i valori dei parametri alle chiamate di ritorno del listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire le azioni appropriate.

   La classe `Event` elenca tutte le interfacce di callback. Ciascuna interfaccia visualizza i parametri restituiti per tale interfaccia.

   Ad esempio:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registra i listener di callback con l&#39;oggetto `MediaPlayer` utilizzando `MediaPlayer.addEventListener`.

   `MediaPlayer` Estensione  `flash.events.IEventDispatcher`, che fa parte dei file core del lettore di Flash e include le funzioni  `addEventListener` e  `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


