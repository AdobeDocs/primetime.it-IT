---
description: Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, come un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, come un annuncio che completa.
seo-description: Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, come un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, come un annuncio che completa.
seo-title: Ascoltare gli eventi di Primetime Player
title: Ascoltare gli eventi di Primetime Player
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Panoramica {#implement-event-listeners-and-callbacks-overview}

I gestori di eventi consentono a TVSDK di rispondere agli eventi. Quando si verifica un evento, il meccanismo eventi di TVSDK chiama il gestore eventi registrato e trasmette le informazioni sull&#39;evento al gestore.

Il runtime di Flash fornisce un meccanismo di eventi generico, che TVSDK utilizza e definisce anche una serie di eventi personalizzati. L&#39;applicazione deve implementare i listener di eventi per gli eventi TVSDK che interessano l&#39;applicazione.

Per un elenco completo degli eventi per l&#39;analisi dei video, consultate [Track Core Video Playback](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html).

1. Determinare gli eventi che l&#39;applicazione deve ascoltare.

   * **Eventi** richiesti: Ascoltare tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >L&#39;evento di riproduzione `MediaPlayerStatusChangeEvent.STATUS_CHANGE` fornisce lo stato del lettore, inclusi gli errori. Uno qualsiasi degli stati potrebbe influenzare il prossimo passo del giocatore.

   * **Altri eventi**: Facoltativo, a seconda dell’applicazione in uso.

      Ad esempio, se si incorpora della pubblicità nella riproduzione, ascoltare tutti gli eventi `AdBreakPlaybackEvent` e `AdPlaybackEvent`.

1. Implementare i listener di eventi per ogni evento.

   TVSDK restituisce i valori dei parametri ai callback dei listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire le azioni appropriate.

   La classe `Event` elenca tutte le interfacce di callback. Ogni interfaccia visualizza i parametri restituiti per tale interfaccia.

   Ad esempio:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registrare i listener di callback con l&#39;oggetto `MediaPlayer` utilizzando `MediaPlayer.addEventListener`.

   `MediaPlayer` extension  `flash.events.IEventDispatcher`, che fa parte dei file core del lettore Flash e include le funzioni  `addEventListener` e  `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


