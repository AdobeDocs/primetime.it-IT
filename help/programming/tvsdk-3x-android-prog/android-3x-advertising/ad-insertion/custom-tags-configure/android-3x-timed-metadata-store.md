---
description: L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
seo-description: L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
seo-title: Archiviare gli oggetti metadati temporizzati durante l'invio
title: Archiviare gli oggetti metadati temporizzati durante l'invio
uuid: 3d0ed022-829d-474e-83a9-152caeb5b317
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Archiviare gli oggetti metadati temporizzati durante l&#39;invio {#store-timed-metadata-objects-as-they-are-dispatched}

L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.

Durante l’analisi del contenuto, che avviene prima della riproduzione, TVSDK identifica i tag sottoscritti e comunica all’applicazione questi tag.

>[!TIP]
>
>L&#39;ora associata a ciascun `TimedMetadata` è l&#39;ora locale nella timeline della riproduzione.

Per memorizzare gli oggetti metadati temporizzati durante l&#39;invio:

1. Tenere traccia del tempo di riproduzione corrente.
1. Corrisponde il tempo di riproduzione corrente agli oggetti `TimedMetadata` inviati.

1. Utilizzate `TimedMetadata` dove l&#39;ora di inizio è uguale all&#39;ora di riproduzione locale corrente.

   L&#39;esempio seguente mostra come salvare gli oggetti `TimedMetadata` in un `ArrayList`.

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

