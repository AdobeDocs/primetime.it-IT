---
description: Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, è possibile nasconderla e visualizzarla nuovamente utilizzando un metodo TVSDK o manualmente.
title: Nascondere una visualizzazione video
exl-id: 92354cd3-f0ed-4434-a7af-a3545e0e2460
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Nascondere una visualizzazione video{#hide-a-video-view}

Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, è possibile nasconderla e visualizzarla nuovamente utilizzando un metodo TVSDK o manualmente.

È necessario mettere in pausa un video prima di cancellarlo o spostarlo dalla visualizzazione.
* Opzione 1: cancellare il fotogramma video con `MediaPlayer.clearVideo`&#x200B; e sostituite il fotogramma in un secondo momento.
   * Metti in pausa il video che desideri nascondere.
   * Rimuovi il fotogramma video visualizzato chiamando `MediaPlayer.clearVideo`.
   * Per ripristinare `MediaPlayer` in modo che possa essere riprodotto di nuovo, chiama `replaceCurrentResource` o `replaceCurrentItem`.
* Opzione 2: spostare il `MediaPlayer` visualizzare lo schermo e riportarlo indietro in un secondo momento senza doverlo sostituire.
   * Metti in pausa il video che desideri nascondere.
   * Spostate la vista fuori dallo stage. Ad esempio:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Per visualizzare nuovamente il video, spostate la vista nell&#39;area di visualizzazione.
