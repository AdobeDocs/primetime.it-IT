---
description: È possibile utilizzare TVSDK per recuperare informazioni sul supporto che è possibile visualizzare sulla barra di ricerca.
title: Visualizza la durata, l'ora corrente e il tempo rimanente del video
exl-id: 490bfa22-6df6-44a3-8e0d-9bb5939ae881
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Visualizza la durata, l&#39;ora corrente e il tempo rimanente del video{#display-the-duration-current-time-and-remaining-time-of-the-video}

È possibile utilizzare TVSDK per recuperare informazioni sul supporto che è possibile visualizzare sulla barra di ricerca.

1. Attendi che il lettore sia nello stato INIZIALIZZATO.
1. Recupera il tempo corrente della testina di riproduzione utilizzando `MediaPlayer.currentTime` proprietà.

   Restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale in millisecondi. Il tempo viene calcolato rispetto al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci o interruzioni pubblicitarie unite nel flusso principale. Per i flussi live/lineari, il tempo restituito è sempre nell’intervallo della finestra di riproduzione.

   ```
   function get currentTime():Number;
   ```

1. Recupera l’intervallo di riproduzione del flusso e determina la durata.
   1. Utilizza il `mediaPlayer.playbackRange` per ottenere l&#39;intervallo di tempo della timeline virtuale.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analizza l’intervallo di tempo utilizzando `mediacore.utils.TimeRange`.
   1. Per determinare la durata, sottrarre l&#39;inizio dalla fine dell&#39;intervallo.

      Ciò include la durata del contenuto aggiuntivo inserito nel flusso (annunci).

      Per VOD, l’intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo inserito nel flusso (annunci).

      Per una risorsa lineare/live, l’intervallo rappresenta l’intervallo della finestra di riproduzione e questo intervallo cambia durante la riproduzione.

      TVSDK invia `MediaPlayerItemEvent.ITEM_UPDATED` per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi (incluso l’intervallo di riproduzione) sono stati aggiornati.

1. Utilizzare i metodi disponibili in `MediaPlayer` e `HSlider` classe disponibile pubblicamente nell’SDK di Flex per impostare i parametri della barra di ricerca.

1. Utilizzare un timer per recuperare periodicamente l&#39;ora corrente e aggiornare `SeekBar`.
