---
description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.
title: Aggiungi i listener per le notifiche dei metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Aggiungi i listener per le notifiche dei metadati temporizzati {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, implementa i listener di notifica appropriati.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `PTTimedMetadataChangedNotification`: Ogni volta che un tag di sottoscrizione univoco viene identificato durante l’analisi del contenuto, TVSDK prepara un nuovo  `PTTimedMetadata` oggetto e invia questa notifica.

   L&#39;oggetto contiene il nome del tag a cui hai effettuato la sottoscrizione, l&#39;ora locale nella riproduzione in cui apparirà il tag e altri dati.

* `PTMediaPlayerTimeChangeNotification` : Per i flussi in diretta/lineare in cui il manifesto/playlist si aggiorna periodicamente, potrebbero essere visualizzati tag personalizzati aggiuntivi nella playlist/manifesto aggiornato, pertanto è possibile aggiungere  `TimedMetadata` oggetti aggiuntivi alla  `MediaPlayerItem.timedMetadata` proprietà.

   Questo evento notifica l&#39;applicazione quando si verifica questa situazione.

   Recupera i metadati temporizzati in uno dei seguenti modi.

   * Imposta l&#39;applicazione per aggiungersi come listener alla notifica `PTTimedMetadataChangedNotification` e recupera l&#39;oggetto utilizzando `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Accedi alla proprietà `timedMetadataCollection` di `PTMediaPlayerItem`, che è costituita da tutti gli oggetti `PTTimedMetadata` notificati finora.