---
description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.
title: Aggiungi i listener per le notifiche dei metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Aggiungi i listener per le notifiche dei metadati temporizzati {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `onTimedMetadata`: Ogni volta che un tag di sottoscrizione univoco viene identificato durante l’analisi del contenuto, TVSDK prepara un nuovo  `TimedMetadata` oggetto e invia questo evento.

   L&#39;oggetto contiene il nome del tag a cui hai effettuato la sottoscrizione, l&#39;ora locale nella riproduzione in cui apparirà il tag e altri dati.

   Ascolta gli eventi.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener =  
     new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
   
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() !=  
                      null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

I metadati ID3 utilizzano lo stesso listener onTimedMetadata per indicare la presenza di un tag ID3. Tuttavia, questo non deve causare confusione, perché è possibile utilizzare la proprietà `type` di un oggetto `TimedMetadata` per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, consulta [ID3 tags](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
