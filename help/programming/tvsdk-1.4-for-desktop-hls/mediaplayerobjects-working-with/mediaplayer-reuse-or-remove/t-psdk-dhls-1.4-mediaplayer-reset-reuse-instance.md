---
description: Quando si reimposta un'istanza MediaPlayer, viene restituito al relativo stato IDLE non inizializzato come definito in MediaPlayerStatus.
title: Reimpostare o riutilizzare un'istanza MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# Reimposta o riutilizza un&#39;istanza MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza MediaPlayer non più necessaria.

Quando si reimposta un&#39;istanza MediaPlayer, viene restituito al relativo stato IDLE non inizializzato come definito in MediaPlayerStatus.

Questa operazione è utile nei casi seguenti:

* Desideri riutilizzare un&#39;istanza `MediaPlayer` ma devi caricare una nuova `MediaResource` (contenuto video) e sostituire l&#39;istanza precedente.

   La reimpostazione consente di riutilizzare l’istanza `MediaPlayer` senza sovraccaricare le risorse rilasciate, ricreare l’ `MediaPlayer` e riallocare le risorse. I metodi `replaceCurrentItem` e `replaceCurrentResource` eseguono automaticamente questi passaggi senza dover chiamare il metodo reset.

* Quando il `MediaPlayer` ha uno stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

1. Invoca `reset` per restituire l&#39;istanza `MediaPlayer` al suo stato non inizializzato:

   ```
   function reset():void; 
   ```

1. Utilizza `MediaPlayer.replaceCurrentItem` o `MediaPlayer.replaceCurrentResource` per caricare un altro `MediaResource`.

   >[!TIP]
   >
   >Per cancellare un errore, carica lo stesso `MediaResource`.

1. Quando ricevi il `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con lo stato `PREPARED`, avvia la riproduzione.
