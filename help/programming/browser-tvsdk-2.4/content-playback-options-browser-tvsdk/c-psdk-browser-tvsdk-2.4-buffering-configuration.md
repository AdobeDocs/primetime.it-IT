---
description: Per fornire un’esperienza di visualizzazione più fluida, il browser TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.
seo-description: Per fornire un’esperienza di visualizzazione più fluida, il browser TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.
seo-title: Buffering
title: Buffering
uuid: 9937731d-013e-41e9-a4c9-f7a54a5e654d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Buffering{#buffering}

Per fornire un’esperienza di visualizzazione più fluida, il browser TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.

Browser TVSDK definisce un buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale entro il quale, prima dell&#39;avvio della riproduzione del supporto, almeno 2 secondi. Dopo le chiamate dell&#39;applicazione `play` ma prima dell&#39;inizio della riproduzione, Browser TVSDK esegue il buffer dei supporti fino al tempo iniziale per dare un avvio uniforme all&#39;avvio effettivo della riproduzione.

## Impostare i tempi di buffering {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non impostate i parametri di controllo del buffer prima dell&#39;inizio della riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

* Per utilizzare i parametri del buffer, utilizzare l&#39;attributo `bufferControlParameters` di MediaPlayer.

   Ad esempio, per impostare il buffer iniziale su 2 secondi e il tempo del buffer di riproduzione su 30 secondi:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Criteri tempo di buffering {#section_7EF2947931654CCC8DAB9172391FA4EB}

A seconda dell’ambiente (incluso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare criteri di buffering diversi per il lettore, ad esempio modificare la durata minima del buffering iniziale e del buffering di riproduzione.

Dopo aver chiamato `play`, il lettore multimediale inizia la memorizzazione del video nel buffer. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l&#39;intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo aver inserito nel buffer i pochi secondi iniziali, la riproduzione inizia.

Durante il rendering del video, Browser TVSDK continua a bufferizzare i nuovi frammenti fino a quando non viene memorizzato nel buffer la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza corrente del buffer scende al di sotto del tempo del buffer di riproduzione, il lettore scaricherà altri frammenti. Una volta che la lunghezza corrente del buffer è superiore di alcuni secondi al tempo del buffer di riproduzione, Browser TVSDK interromperà il download dei frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è elevato, potrebbe fornire all&#39;utente un lungo tempo iniziale di buffering prima dell&#39;avvio. Ciò potrebbe fornire una riproduzione uniforme per un periodo di tempo più lungo; tuttavia, se le condizioni della rete non sono soddisfacenti, la riproduzione iniziale potrebbe essere ritardata.

