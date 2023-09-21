---
description: Dopo aver utilizzato una visualizzazione MediaPlayer per riprodurre il video, è possibile nasconderla e visualizzarla nuovamente utilizzando un metodo TVSDK o manualmente.
title: Nascondere una visualizzazione video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
