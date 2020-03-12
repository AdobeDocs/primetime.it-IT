---
description: Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.
seo-description: Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.
seo-title: Aggiunta di listener per le notifiche di metadati temporizzate
title: Aggiunta di listener per le notifiche di metadati temporizzate
uuid: 336882e7-e2d8-49b8-a23d-f236c7e6a594
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Aggiunta di listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.

Potete monitorare i metadati temporizzati ascoltando `onTimedMetadata`, per notificare all’applicazione l’attività correlata. Ogni volta che viene identificato un tag di sottoscrizione univoco durante l&#39;analisi del contenuto, TVSDK prepara un nuovo `TimedMetadata` oggetto e invia questo evento. L&#39;oggetto contiene il nome del tag a cui avete effettuato la sottoscrizione, l&#39;ora locale nella riproduzione in cui apparirà il tag e altri dati.

1. Ascoltare gli eventi.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
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
           } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

I metadati ID3 utilizzano lo stesso `onTimedMetadata` listener per indicare la presenza di un tag ID3. Ciò non deve tuttavia creare confusione, perché è possibile utilizzare la `TimedMetadata` `type` proprietà per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, vedere [ID3 tags](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md).