---
description: Puoi usare TVSDK per recuperare informazioni sui file multimediali da visualizzare sulla barra di ricerca.
title: Visualizza la durata, l'ora corrente e il tempo rimanente del video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Visualizza la durata, l&#39;ora corrente e il tempo rimanente del video{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puoi usare TVSDK per recuperare informazioni sui file multimediali da visualizzare sulla barra di ricerca.

1. Attendi che il lettore sia nello stato INITIALIZZATO.
1. Recupera l&#39;ora corrente dell&#39;indicatore di riproduzione utilizzando la proprietà `MediaPlayer.currentTime` .

   Restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale, in millisecondi. Il tempo viene calcolato in base al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci o interruzioni pubblicitarie unite nel flusso principale. Per i flussi in tempo reale/lineare, il tempo restituito è sempre nell&#39;intervallo della finestra di riproduzione.

   ```
   function get currentTime():Number;
   ```

1. Recupera l&#39;intervallo di riproduzione del flusso e determina la sua durata.
   1. Utilizzare la proprietà `mediaPlayer.playbackRange` per ottenere l&#39;intervallo di tempo della timeline virtuale.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analizza l’intervallo di tempo utilizzando `mediacore.utils.TimeRange`.
   1. Per determinare la durata, sottraete l’inizio dalla fine dell’intervallo.

      Ciò include la durata del contenuto aggiuntivo inserito nel flusso (annunci).

      Per VOD, l’intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo inserito nel flusso (annunci).

      Per una risorsa lineare/live, l’intervallo rappresenta l’intervallo della finestra di riproduzione e questo intervallo cambia durante la riproduzione.

      TVSDK invia un evento `MediaPlayerItemEvent.ITEM_UPDATED` per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi (compreso l’intervallo di riproduzione) sono stati aggiornati.

1. Utilizza i metodi disponibili nella classe `MediaPlayer` e `HSlider` che sono disponibili pubblicamente nell’SDK di Flex per impostare i parametri della barra di ricerca.

1. Utilizzare un timer per recuperare periodicamente l&#39;ora corrente e aggiornare `SeekBar`.
