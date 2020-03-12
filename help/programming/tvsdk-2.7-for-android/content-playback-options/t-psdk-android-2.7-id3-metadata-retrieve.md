---
description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L'applicazione può estrarre dati dal tag .
seo-description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L'applicazione può estrarre dati dal tag .
seo-title: ID3, tag
title: ID3, tag
uuid: 3fa199cd-668d-4d26-928f-074b6114b84c
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# ID3, tag {#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L&#39;applicazione può estrarre dati dal tag .

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264) in qualsiasi codifica possibile (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* TYPE = ID3
* NAME = ID3

1. Implementare un listener di eventi per `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registrarlo con l&#39; `MediaPlayer` oggetto.

   TVSDK chiama questo listener quando rileva `ID3` i metadati.

   >[!TIP]
   >
   >I suggerimenti per gli annunci personalizzati utilizzano lo stesso `onTimedMetadata` evento per indicare il rilevamento di un nuovo tag. Ciò non deve creare confusione perché vengono rilevati segnali pubblicitari personalizzati a livello di manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, vedere [Tag](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md)personalizzati.


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
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```

