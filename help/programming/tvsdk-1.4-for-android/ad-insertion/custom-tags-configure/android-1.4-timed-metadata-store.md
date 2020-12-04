---
description: L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
seo-description: L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
seo-title: Archiviare gli oggetti metadati temporizzati durante l'invio
title: Archiviare gli oggetti metadati temporizzati durante l'invio
uuid: 0e6d2a42-37a8-477e-b925-66bbc23445c1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Archiviare gli oggetti metadati temporizzati durante l&#39;invio {#store-timed-metadata-objects-as-they-are-dispatched}

L’applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.

Durante l’analisi del contenuto, che avviene prima della riproduzione, TVSDK identifica i tag sottoscritti e comunica all’applicazione questi tag. L&#39;ora associata a ciascun `TimedMetadata` è l&#39;ora locale nella timeline della riproduzione.

L&#39;applicazione deve completare le seguenti attività:

1. Tenere traccia del tempo di riproduzione corrente.
1. Corrisponde il tempo di riproduzione corrente agli oggetti `TimedMetadata` inviati.

1. Utilizzate `TimedMetadata` dove l&#39;ora di inizio è uguale all&#39;ora di riproduzione locale corrente.

   L&#39;esempio seguente mostra come salvare gli oggetti `TimedMetadata` in un `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

