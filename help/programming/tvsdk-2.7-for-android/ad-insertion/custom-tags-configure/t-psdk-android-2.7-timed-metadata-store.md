---
description: L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
seo-description: L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
seo-title: Archiviare gli oggetti metadati temporizzati durante l'invio
title: Archiviare gli oggetti metadati temporizzati durante l'invio
uuid: 0d0ddfea-6f32-467d-91bc-f18ceadcd842
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Archiviare gli oggetti metadati temporizzati durante l&#39;invio {#store-timed-metadata-objects-as-they-are-dispatched}

L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.

Durante l’analisi del contenuto, che avviene prima della riproduzione, TVSDK identifica i tag sottoscritti e comunica all’applicazione questi tag.

>[!TIP]
>
>L’ora associata a ciascuna `TimedMetadata` è l’ora locale nella timeline di riproduzione.

Per memorizzare gli oggetti metadati temporizzati durante l&#39;invio:

1. Tenere traccia del tempo di riproduzione corrente.
1. Associare il tempo di riproduzione corrente agli `TimedMetadata` oggetti inviati.

1. Utilizzare il `TimedMetadata` punto in cui l&#39;ora di inizio è uguale all&#39;ora di riproduzione locale corrente.

   L&#39;esempio seguente mostra come salvare `TimedMetadata` gli oggetti in un `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

