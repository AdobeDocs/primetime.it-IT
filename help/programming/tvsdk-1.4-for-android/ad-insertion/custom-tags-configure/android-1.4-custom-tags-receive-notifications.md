---
description: Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.
title: Aggiungere listener per le notifiche di metadati temporizzate
exl-id: febf354b-2a25-4108-abd9-6ff1e09cee39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Aggiungere listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, implementa i listener di eventi appropriati.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione l’attività correlata:

* `onTimedMetadata`: ogni volta che durante l’analisi del contenuto viene identificato un tag sottoscritto univoco, TVSDK prepara un nuovo `TimedMetadata` e invia questo evento.

   L’oggetto contiene il nome del tag a cui ti sei iscritto, l’ora locale nella riproduzione in cui verrà visualizzato il tag e altri dati.

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

I metadati ID3 utilizzano lo stesso listener onTimedMetadata per indicare la presenza di un tag ID3. Tuttavia, questo non dovrebbe causare confusione, perché è possibile utilizzare un `TimedMetadata` dell&#39;oggetto `type` per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, consulta [Tag ID3](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
