---
description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.
seo-description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.
seo-title: Aggiunta di listener per le notifiche di metadati temporizzate
title: Aggiunta di listener per le notifiche di metadati temporizzate
uuid: b6939011-a6ff-4342-8e7c-3a0c805ee91c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Aggiunta di listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.

Potete monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `PTTimedMetadataChangedNotification`: Ogni volta che viene identificato un tag di sottoscrizione univoco durante l&#39;analisi del contenuto, TVSDK prepara un nuovo `PTTimedMetadata` oggetto e invia questa notifica.

   L&#39;oggetto contiene il nome del tag a cui avete effettuato la sottoscrizione, l&#39;ora locale nella riproduzione in cui apparirà il tag e altri dati.

* `PTMediaPlayerTimeChangeNotification` : Per i flussi live/lineari in cui il manifest/playlist viene aggiornato periodicamente, è possibile che nella playlist/nel manifesto aggiornato vengano visualizzati tag personalizzati aggiuntivi, per cui è possibile aggiungere `TimedMetadata` oggetti aggiuntivi alla `MediaPlayerItem.timedMetadata` proprietà.

   Questo evento notifica l’applicazione in caso di evento.

   Recuperate i metadati temporizzati in uno dei modi seguenti.

   * Impostate l&#39;applicazione per aggiungersi come listener alla `PTTimedMetadataChangedNotification` notifica e recuperate l&#39;oggetto utilizzando `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Accedere alla `timedMetadataCollection` proprietà di `PTMediaPlayerItem`, costituita da tutti gli `PTTimedMetadata` oggetti notificati finora.