---
description: Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.
title: Aggiungere listener per le notifiche di metadati temporizzate
exl-id: e4be34b6-0f29-45b8-a089-b79b41daeada
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Aggiungere listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.

È possibile monitorare i metadati temporizzati ascoltando `onTimedMetadata`, che notifica all&#39;applicazione l&#39;attività correlata. Ogni volta che durante l’analisi del contenuto viene identificato un tag sottoscritto univoco, TVSDK prepara un nuovo `TimedMetadata` e invia questo evento. L’oggetto contiene il nome del tag a cui ti sei iscritto, l’ora locale nella riproduzione in cui verrà visualizzato il tag e altri dati.

Ascolta gli eventi.

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

I metadati ID3 utilizzano lo stesso `onTimedMetadata` per indicare la presenza di un tag ID3. Tuttavia, questo non dovrebbe causare confusione, perché è possibile utilizzare il `TimedMetadata` `type` per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, consulta [Tag ID3](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).
