---
description: Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, potete nasconderlo e visualizzarlo nuovamente utilizzando un metodo TVSDK o manualmente.
seo-description: Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, potete nasconderlo e visualizzarlo nuovamente utilizzando un metodo TVSDK o manualmente.
seo-title: Nascondere una visualizzazione video
title: Nascondere una visualizzazione video
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Nascondere una visualizzazione video{#hide-a-video-view}

Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, potete nasconderlo e visualizzarlo nuovamente utilizzando un metodo TVSDK o manualmente.

È necessario mettere in pausa un video prima di cancellarlo o spostarlo dal display.
* Opzione 1: Cancellate il fotogramma video con `MediaPlayer.clearVideo`&#x200B; e sostituite il fotogramma in un secondo momento.
   * Metti in pausa il video che vuoi nascondere.
   * Rimuovete il fotogramma video visualizzato chiamando `MediaPlayer.clearVideo`.
   * Per ripristinare il `MediaPlayer` sistema in modo che possa essere riprodotto, chiamare `replaceCurrentResource` o `replaceCurrentItem`.
* Opzione 2: Spostare la `MediaPlayer` vista dallo schermo e riportarla in un secondo momento senza dover sostituire la vista.
   * Metti in pausa il video che vuoi nascondere.
   * Spostate la vista fuori dall’area di visualizzazione. Ad esempio:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Per visualizzare nuovamente il video, spostate di nuovo la visualizzazione nell’area di visualizzazione.
