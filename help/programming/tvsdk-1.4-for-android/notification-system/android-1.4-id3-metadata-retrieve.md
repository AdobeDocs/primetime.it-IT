---
description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L'applicazione può estrarre dati dal tag .
seo-description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L'applicazione può estrarre dati dal tag .
seo-title: ID3, tag
title: ID3, tag
uuid: 5e5c5f89-7653-47c1-b9c1-6b9b9b1f8d73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Tag ID3 {#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L&#39;applicazione può estrarre dati dal tag .

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264), in qualsiasi codifica possibile (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* InfoCode = 303007
* TYPE = ID3
* NAME = not present
* ID = 0

1. Implementare un listener di eventi per `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registrarlo con l&#39;oggetto `MediaPlayer`.

   TVSDK chiama questo listener quando rileva i metadati ID3.

   >[!NOTE]
   >
   >I suggerimenti per gli annunci personalizzati utilizzano lo stesso evento `onTimedMetadata` per indicare il rilevamento di un nuovo tag. Ciò non deve creare confusione perché vengono rilevati segnali pubblicitari personalizzati a livello di manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, consultate custom-tags-configure .

1. Recuperate i metadati.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```

