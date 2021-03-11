---
description: Per fornire un’esperienza di visualizzazione più fluida, il browser TVSDK a volte carica il flusso video. Puoi configurare il modo in cui il lettore buffer.
title: Buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---


# Buffering{#buffering}

Per fornire un’esperienza di visualizzazione più fluida, il browser TVSDK a volte carica il flusso video. Puoi configurare il modo in cui il lettore buffer.

Il browser TVSDK definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale entro il quale, prima che il supporto inizi la riproduzione, di almeno 2 secondi. Dopo che l&#39;applicazione chiama `play` ma prima dell&#39;inizio della riproduzione, il browser TVSDK carica il contenuto multimediale fino al tempo iniziale per dare un avvio fluido quando inizia effettivamente la riproduzione.

## Imposta i tempi di buffering {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer fornisce i metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima della riproduzione iniziale, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo di buffer di riproduzione in corso.

* Per utilizzare i parametri del buffer, utilizzare l&#39;attributo `bufferControlParameters` di MediaPlayer.

   Ad esempio, per impostare il buffer iniziale a 2 secondi e il tempo del buffer di riproduzione a 30 secondi:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Criteri per il tempo di buffering {#section_7EF2947931654CCC8DAB9172391FA4EB}

A seconda dell’ambiente (compreso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare diversi criteri di buffering per il lettore, ad esempio la modifica della durata minima per il buffering iniziale e per il buffering di riproduzione continuo.

Dopo aver chiamato `play`, il lettore multimediale inizia a bufferizzare il video. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l&#39;intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo il buffering dei pochi secondi iniziali, inizia la riproduzione.

Durante il rendering del video, il browser TVSDK continua a buffer dei nuovi frammenti fino a quando non viene bufferizzata la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza corrente del buffer scende al di sotto del tempo di riproduzione del buffer, il lettore scarica ulteriori frammenti. Una volta che la lunghezza corrente del buffer è superiore di alcuni secondi al tempo del buffer di riproduzione, il browser TVSDK smetterà di scaricare i frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è elevato, potrebbe fornire all&#39;utente un lungo tempo iniziale di buffering prima dell&#39;avvio. Ciò potrebbe fornire una riproduzione uniforme per un periodo di tempo più lungo; tuttavia, se le condizioni di rete sono scadenti, la riproduzione iniziale potrebbe essere ritardata.

