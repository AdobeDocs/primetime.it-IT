---
description: L'applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.
title: Archiviare gli oggetti metadati temporizzati durante l'invio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Archiviare gli oggetti metadati temporizzati durante l&#39;invio {#store-timed-metadata-objects-as-they-are-dispatched}

L&#39;applicazione deve utilizzare gli oggetti TimedMetadata appropriati ai momenti opportuni.

Durante l’analisi del contenuto, che avviene prima della riproduzione, TVSDK identifica i tag sottoscritti e notifica all’applicazione tali tag.

>[!TIP]
>
>L&#39;ora associata a ogni `TimedMetadata` è l&#39;ora locale nella timeline di riproduzione.

Per memorizzare gli oggetti metadati temporizzati durante l’invio:

1. Tenere traccia del tempo di riproduzione corrente.
1. Associa il tempo di riproduzione corrente agli oggetti `TimedMetadata` inviati.

1. Utilizzare il valore `TimedMetadata` in cui l&#39;ora di inizio è uguale al tempo di riproduzione locale corrente.

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

