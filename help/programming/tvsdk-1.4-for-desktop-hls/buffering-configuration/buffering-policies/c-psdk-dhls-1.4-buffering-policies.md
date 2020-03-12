---
description: Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.
seo-description: Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.
seo-title: Criteri tempo di buffer
title: Criteri tempo di buffer
uuid: 8d3ce9be-cca4-485e-ba66-d2f2aa6822dd
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Criteri tempo di buffer {#buffering-time-policies}

Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.

TVSDK definisce un buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale entro il quale, prima dell&#39;avvio della riproduzione del supporto, almeno 5 secondi. Dopo le chiamate dell’applicazione `play` ma prima dell’inizio della riproduzione, TVSDK esegue il buffer dei contenuti multimediali fino al tempo iniziale per dare un avvio corretto all’avvio effettivo della riproduzione.

È possibile modificare i tempi del buffer definendo nuovi criteri di buffering.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

A seconda dell’ambiente (incluso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare criteri di buffering diversi per il lettore, ad esempio modificare la durata minima del buffering iniziale e del buffering di riproduzione.

Dopo aver chiamato `play`, il lettore multimediale inizia la memorizzazione del video nel buffer. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l&#39;intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo aver inserito nel buffer i pochi secondi iniziali, la riproduzione inizia.

Durante il rendering del video, TVSDK continua a bufferizzare i nuovi frammenti fino a quando non viene memorizzato nel buffer la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza corrente del buffer scende al di sotto del tempo del buffer di riproduzione, il lettore scaricherà altri frammenti. Quando la lunghezza corrente del buffer è superiore di alcuni secondi al tempo del buffer di riproduzione, TVSDK interrompe il download dei frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è elevato, potrebbe fornire all&#39;utente un lungo tempo iniziale di buffering prima dell&#39;avvio. Ciò potrebbe fornire una riproduzione uniforme per un periodo di tempo più lungo; tuttavia, se le condizioni della rete non sono soddisfacenti, la riproduzione iniziale potrebbe essere ritardata.

