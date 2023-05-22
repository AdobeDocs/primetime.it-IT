---
description: Quando si reimposta un'istanza MediaPlayer, questa viene ripristinata allo stato IDLE non inizializzato definito in MediaPlayerStatus.
title: Reimpostare o riutilizzare un'istanza MediaPlayer
exl-id: e06a0052-ce0a-4a6c-8ebc-0666b109cf07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Reimpostare o riutilizzare un&#39;istanza MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

Quando si reimposta un&#39;istanza MediaPlayer, questa viene ripristinata allo stato IDLE non inizializzato definito in MediaPlayerStatus.

Questa operazione è utile nei seguenti casi:

* Si desidera riutilizzare un `MediaPlayer` ma deve caricare un nuovo `MediaResource` (contenuto video) e sostituisci l’istanza precedente.

   Il ripristino consente di riutilizzare `MediaPlayer` senza il sovraccarico di rilasciare le risorse, ricreando il `MediaPlayer`e la riallocazione delle risorse. Il `replaceCurrentItem` e `replaceCurrentResource` i metodi eseguono automaticamente questi passaggi senza dover chiamare il metodo reset.

* Quando `MediaPlayer` ha uno stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l’unico modo per recuperare dallo stato ERROR.

1. Chiamata `reset` per restituire il `MediaPlayer` istanza al relativo stato non inizializzato:

   ```
   function reset():void; 
   ```

1. Utilizzare `MediaPlayer.replaceCurrentItem` o `MediaPlayer.replaceCurrentResource` per caricare un altro `MediaResource`.

   >[!TIP]
   >
   >Per cancellare un errore, carica lo stesso `MediaResource`.

1. Quando ricevi il `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con `PREPARED` stato, avvia la riproduzione.
