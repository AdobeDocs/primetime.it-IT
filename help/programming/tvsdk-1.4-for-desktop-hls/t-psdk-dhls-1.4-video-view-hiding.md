---
description: Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, è possibile nasconderlo e visualizzarlo nuovamente utilizzando un metodo TVSDK o manualmente.
title: Nascondere una visualizzazione video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---


# Nascondere una visualizzazione video{#hide-a-video-view}

Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, è possibile nasconderlo e visualizzarlo nuovamente utilizzando un metodo TVSDK o manualmente.

È necessario mettere in pausa un video prima di cancellarlo o spostarlo dal display.
* Opzione 1: Cancella il fotogramma video con `MediaPlayer.clearVideo` &#x200B; e sostituiscilo successivamente.
   * Sospendi il video che desideri nascondere.
   * Rimuovi il fotogramma video visualizzato chiamando `MediaPlayer.clearVideo`.
   * Per reimpostare il `MediaPlayer` in modo che possa essere riprodotto, chiamare `replaceCurrentResource` o `replaceCurrentItem`.
* Opzione 2: Spostare la visualizzazione `MediaPlayer` dallo schermo e riportarla in un secondo momento senza sostituirla.
   * Sospendi il video che desideri nascondere.
   * Spostare la vista fuori dal palco. Ad esempio:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Per visualizzare nuovamente il video, sposta nuovamente la visualizzazione nell’area di visualizzazione.
