---
description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.
seo-description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.
seo-title: Aggiunta di listener per le notifiche di metadati temporizzate
title: Aggiunta di listener per le notifiche di metadati temporizzate
uuid: cd7a5936-d63a-4711-ac16-2d79bac099a3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Aggiunta di listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.

Potete monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `onTimedMetadata`: Ogni volta che viene identificato un tag di sottoscrizione univoco durante l&#39;analisi del contenuto, TVSDK prepara un nuovo  `TimedMetadata` oggetto e invia questo evento.

   L&#39;oggetto contiene il nome del tag a cui avete effettuato la sottoscrizione, l&#39;ora locale nella riproduzione in cui apparirà il tag e altri dati.

   Ascoltare gli eventi.

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

I metadati ID3 utilizzano lo stesso listener onTimedMetadata per indicare la presenza di un tag ID3. Ciò non deve creare confusione, tuttavia, perché è possibile utilizzare una proprietà `TimedMetadata` dell&#39;oggetto `type` per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, vedere [ID3 tags](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
