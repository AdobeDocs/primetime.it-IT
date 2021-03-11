---
description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag .
title: Tag ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Tag ID3 {#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell’artista. TVSDK rileva i tag ID3 a livello di segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag .

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264) in qualsiasi codifica possibile (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* TYPE = ID3
* NAME = ID3

1. Implementa un listener di eventi per `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registralo con l&#39;oggetto `MediaPlayer` .

   TVSDK chiama questo listener quando rileva i metadati `ID3`.

   >[!TIP]
   >
   >I suggerimenti per gli annunci personalizzati utilizzano lo stesso evento `onTimedMetadata` per indicare il rilevamento di un nuovo tag. Questo non deve causare confusione perché vengono rilevati suggerimenti di annunci personalizzati a livello di manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, consulta [Tag personalizzati](../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/custom-tags-configure/android-3x-custom-tags-configure.md).

1. Recupera i metadati.

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
