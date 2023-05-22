---
description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.
title: Aggiungere listener per le notifiche di metadati temporizzate
exl-id: 259af856-797b-4a50-9add-f72132831ba1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Aggiungere listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione l’attività correlata:

* `PTTimedMetadataChangedNotification`: ogni volta che durante l’analisi del contenuto viene identificato un tag sottoscritto univoco, TVSDK prepara un nuovo `PTTimedMetadata` e invia questa notifica.

   L’oggetto contiene il nome del tag a cui ti sei iscritto, l’ora locale nella riproduzione in cui verrà visualizzato il tag e altri dati.

* `PTMediaPlayerTimeChangeNotification` : per i flussi live/lineari in cui il manifesto/la playlist viene aggiornato periodicamente, nella playlist/il manifesto aggiornato potrebbero essere visualizzati tag personalizzati aggiuntivi `TimedMetadata` Gli oggetti possono essere aggiunti al `MediaPlayerItem.timedMetadata` proprietà.

   Questo evento avvisa l&#39;applicazione quando si verifica.

   Recupera i metadati temporizzati in uno dei seguenti modi.

   * Imposta l’applicazione per aggiungersi come listener al `PTTimedMetadataChangedNotification` e recuperare l&#39;oggetto utilizzando `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Accedere a `timedMetadataCollection` proprietà di `PTMediaPlayerItem`, costituito da tutte le `PTTimedMetadata` oggetti notificati finora.
