---
description: Per offrire un’esperienza di visualizzazione più fluida, a volte il browser TVSDK memorizza in buffer il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.
title: Buffering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Buffering{#buffering}

Per offrire un’esperienza di visualizzazione più fluida, a volte il browser TVSDK memorizza in buffer il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.

Il TVSDK del browser definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo iniziale del buffer entro il quale, prima dell’avvio della riproduzione del contenuto multimediale, deve essere di almeno 2 secondi. Dopo le chiamate dell’applicazione `play` ma prima dell’inizio della riproduzione, il browser TVSDK memorizza in buffer il contenuto multimediale fino al momento iniziale per dare un inizio fluido quando inizia effettivamente la riproduzione.

## Impostare i tempi di buffering {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering della riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima di iniziare la riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

* Per utilizzare i parametri del buffer, utilizzare il `bufferControlParameters` attributo.

  Ad esempio, per impostare il buffer iniziale su 2 secondi e il tempo del buffer di riproduzione su 30 secondi:

  ```js
  var params = new AdobePSDK.BufferControlParameters(2000, 30000);
  ```

## Criteri tempo di buffering {#section_7EF2947931654CCC8DAB9172391FA4EB}

A seconda dell’ambiente in uso (compreso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare criteri di buffering diversi per il lettore, ad esempio per modificare la durata minima del buffering iniziale e per la riproduzione in corso.

Dopo aver chiamato `play`, il lettore multimediale inizia a memorizzare il video nel buffering. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l’intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo aver inserito nel buffer i pochi secondi iniziali, inizia la riproduzione.

Durante il rendering del video, il browser TVSDK continua a memorizzare nel buffer nuovi frammenti fino a quando non viene inserito nel buffer la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza del buffer corrente scende al di sotto del tempo del buffer di riproduzione, il lettore scarica altri frammenti. Quando la lunghezza del buffer corrente supera di alcuni secondi il tempo del buffer di riproduzione, TVSDK del browser interrompe il download dei frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è alto, potrebbe assegnare all’utente un tempo di buffering iniziale lungo prima di iniziare. Questo potrebbe garantire una riproduzione fluida per un periodo di tempo più lungo; tuttavia, se le condizioni di rete sono scarse, la riproduzione iniziale potrebbe subire ritardi.
