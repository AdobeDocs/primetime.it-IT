---
description: I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell'artista. rileva i tag ID3 a livello del segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag.
title: Tag ID3
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Tag ID3{#id-tags}

I tag ID3 forniscono informazioni su un file audio o video, ad esempio il titolo del file o il nome dell&#39;artista. rileva i tag ID3 a livello del segmento del flusso di trasporto (TS) nei flussi HLS e invia un evento. L’applicazione può estrarre dati dal tag.

>[!IMPORTANT]
>
>TVSDK riconosce i metadati ID3 (versione 2.3.0 o 2.4.0) nei flussi audio (AAC) e video (H.264), in una qualsiasi delle sue possibili codifiche (ASCII, UTF8, UTF16-BE o UTF16-LE). Ignora i tag ID3 che non sono in una delle versioni o dei formati riconosciuti. La codifica non specificata viene trattata come UTF8.

Quando TVSDK rileva i metadati ID3, invia una notifica con i seguenti dati:

* InfoCode = 303007
* TYPE = ID3
* NAME = non presente
* ID = 0

1. Implementare un listener di eventi per `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` e registrarlo con il `MediaPlayer` oggetto.

   TVSDK chiama questo listener quando rileva i metadati ID3.

   >[!NOTE]
   >
   >I suggerimenti degli annunci personalizzati utilizzano lo stesso `onTimedMetadata` per indicare il rilevamento di un nuovo tag. Ciò non dovrebbe causare confusione perché vengono rilevati suggerimenti di annunci personalizzati a livello del manifesto e i tag ID3 sono incorporati nel flusso. Per ulteriori informazioni, consulta custom-tags-configure .

1. Recupera i metadati.

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```
