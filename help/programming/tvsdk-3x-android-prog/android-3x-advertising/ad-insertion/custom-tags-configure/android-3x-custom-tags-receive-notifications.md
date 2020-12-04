---
description: Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.
seo-description: Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.
seo-title: Aggiunta di listener per le notifiche di metadati temporizzate
title: Aggiunta di listener per le notifiche di metadati temporizzate
uuid: bb996b4a-282e-4321-a9e9-513f0df45b70
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Aggiunta di listener per le notifiche di metadati temporizzate {#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, è necessario implementare i listener di eventi appropriati.

È possibile monitorare i metadati temporizzati ascoltando `onTimedMetadata`, che avvisano l&#39;applicazione delle relative attività. Ogni volta che viene identificato un tag di sottoscrizione univoco durante l&#39;analisi del contenuto, TVSDK prepara un nuovo oggetto `TimedMetadata` e invia questo evento. L&#39;oggetto contiene il nome del tag a cui avete effettuato la sottoscrizione, l&#39;ora locale nella riproduzione in cui apparirà il tag e altri dati.

Ascoltare gli eventi.

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

I metadati ID3 utilizzano lo stesso `onTimedMetadata` listener per indicare la presenza di un tag ID3. Ciò non deve tuttavia creare confusione, perché è possibile utilizzare la proprietà `TimedMetadata` `type` per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, vedere [ID3 tags](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).