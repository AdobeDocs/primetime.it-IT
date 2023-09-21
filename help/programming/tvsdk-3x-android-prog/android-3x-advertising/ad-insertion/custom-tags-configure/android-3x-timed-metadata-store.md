---
description: L'applicazione deve utilizzare gli oggetti TimedMetadata appropriati nei momenti appropriati.
title: Archivia gli oggetti metadati temporizzati durante l’invio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Archivia gli oggetti metadati temporizzati durante l’invio {#store-timed-metadata-objects-as-they-are-dispatched}

L&#39;applicazione deve utilizzare gli oggetti TimedMetadata appropriati nei momenti appropriati.

Durante l’analisi del contenuto, che si verifica prima della riproduzione, TVSDK identifica i tag abbonati e ne informa l’applicazione.

>[!TIP]
>
>L’ora associata a ogni `TimedMetadata` è l’ora locale sulla timeline di riproduzione.

Per memorizzare gli oggetti metadati temporizzati durante l’invio:

1. Tieni traccia del tempo di riproduzione corrente.
1. Corrispondenza del tempo di riproduzione corrente con quello inviato `TimedMetadata` oggetti.

1. Utilizza il `TimedMetadata` dove l’ora di inizio è uguale all’ora di riproduzione locale corrente.

   L’esempio seguente mostra come salvare `TimedMetadata` oggetti in un `ArrayList`.

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
