---
description: Potete usare TVSDK per recuperare informazioni sui file multimediali che potete visualizzare sulla barra di ricerca.
seo-description: Potete usare TVSDK per recuperare informazioni sui file multimediali che potete visualizzare sulla barra di ricerca.
seo-title: Visualizzare la durata, l’ora corrente e il tempo rimanente del video
title: Visualizzare la durata, l’ora corrente e il tempo rimanente del video
uuid: 64536ba7-33a1-49f8-a947-5700e1e9c032
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Visualizzare la durata, l’ora corrente e il tempo rimanente del video{#display-the-duration-current-time-and-remaining-time-of-the-video}

Potete usare TVSDK per recuperare informazioni sui file multimediali che potete visualizzare sulla barra di ricerca.

1. Attendi che il tuo giocatore sia nello stato INITIALIZED.
1. Recuperare il tempo corrente dell&#39;indicatore di riproduzione utilizzando la `MediaPlayer.currentTime` proprietà .

   Questo restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale, in millisecondi. L&#39;ora viene calcolata in relazione al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci pubblicitari o interruzioni di annunci nel flusso principale. Per i flussi live/lineari, il tempo restituito è sempre compreso nell&#39;intervallo della finestra di riproduzione.

   ```
   function get currentTime():Number;
   ```

1. Recuperate l’intervallo di riproduzione del flusso e stabilite la durata.
   1. Utilizzare la `mediaPlayer.playbackRange` proprietà per ottenere l&#39;intervallo di tempo della cronologia virtuale.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analizzare l&#39;intervallo di tempo utilizzando `mediacore.utils.TimeRange`.
   1. Per determinare la durata, sottraete l’inizio dalla fine dell’intervallo.

      Ciò include la durata del contenuto aggiuntivo inserito nel flusso (annunci).

      Per il VOD, l&#39;intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo inserito nel flusso (annunci).

      Per una risorsa lineare/live, l&#39;intervallo rappresenta l&#39;intervallo della finestra di riproduzione e questo intervallo cambia durante la riproduzione.

      TVSDK invia un `MediaPlayerItemEvent.ITEM_UPDATED` evento per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi (compreso l’intervallo di riproduzione) sono stati aggiornati.

1. Utilizzate i metodi disponibili in `MediaPlayer` e nella `HSlider` classe che sono disponibili pubblicamente in Flex SDK per impostare i parametri della barra di ricerca.

1. Utilizzare un timer per recuperare periodicamente l&#39;ora corrente e aggiornare il `SeekBar`.
