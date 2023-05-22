---
description: L'applicazione deve utilizzare gli oggetti TimedMetadata appropriati nei momenti appropriati.
title: Archivia gli oggetti metadati temporizzati durante l’invio
exl-id: db8b303a-441e-4cc0-a80d-dc9afda482b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Archivia gli oggetti metadati temporizzati durante l’invio {#store-timed-metadata-objects-as-they-are-dispatched}

L&#39;applicazione deve utilizzare gli oggetti TimedMetadata appropriati nei momenti appropriati.

Durante l’analisi del contenuto, che si verifica prima della riproduzione, TVSDK identifica i tag abbonati e ne informa l’applicazione. L’ora associata a ogni `TimedMetadata` è l’ora locale sulla timeline di riproduzione.

L&#39;applicazione deve completare le seguenti attività:

1. Tieni traccia del tempo di riproduzione corrente.
1. Corrispondenza del tempo di riproduzione corrente con quello inviato `TimedMetadata` oggetti.

1. Utilizza il `TimedMetadata` dove l’ora di inizio è uguale all’ora di riproduzione locale corrente.

   L’esempio seguente mostra come salvare `TimedMetadata` oggetti in un `ArrayList`.

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
