---
description: Per fornire un’esperienza di visualizzazione più fluida, a volte TVSDK carica il flusso video. Puoi configurare il modo in cui il lettore buffer.
title: Criteri per i tempi di buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Criteri per il tempo di buffering {#buffering-time-policies}

Per fornire un’esperienza di visualizzazione più fluida, a volte TVSDK carica il flusso video. Puoi configurare il modo in cui il lettore buffer.

TVSDK definisce un buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale entro il quale, prima che il supporto inizi la riproduzione, di almeno 5 secondi. Dopo che l&#39;applicazione chiama `play` ma prima dell&#39;inizio della riproduzione, TVSDK carica il contenuto multimediale fino al tempo iniziale per dare un avvio fluido quando inizia effettivamente la riproduzione.

È possibile modificare i tempi di buffer definendo nuovi criteri di buffering.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

A seconda dell’ambiente (compreso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare diversi criteri di buffering per il lettore, ad esempio la modifica della durata minima per il buffering iniziale e per il buffering di riproduzione continuo.

Dopo aver chiamato `play`, il lettore multimediale inizia a bufferizzare il video. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l&#39;intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo il buffering dei pochi secondi iniziali, inizia la riproduzione.

Durante il rendering del video, TVSDK continua a creare un buffer per i nuovi frammenti fino a quando non viene bufferizzata la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza corrente del buffer scende al di sotto del tempo di riproduzione del buffer, il lettore scarica ulteriori frammenti. Una volta che la lunghezza corrente del buffer è superiore di alcuni secondi al tempo del buffer di riproduzione, TVSDK smetterà di scaricare i frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è elevato, potrebbe fornire all&#39;utente un lungo tempo iniziale di buffering prima dell&#39;avvio. Ciò potrebbe fornire una riproduzione uniforme per un periodo di tempo più lungo; tuttavia, se le condizioni di rete sono scadenti, la riproduzione iniziale potrebbe essere ritardata.

