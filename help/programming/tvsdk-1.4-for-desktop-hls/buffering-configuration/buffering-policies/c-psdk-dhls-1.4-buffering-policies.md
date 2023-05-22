---
description: Per offrire un’esperienza di visualizzazione più fluida, TVSDK a volte archivia il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.
title: Criteri tempo di buffering
exl-id: 78f1bb9f-3d10-4f05-90dd-5b52eee0feec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Criteri tempo di buffering {#buffering-time-policies}

Per offrire un’esperienza di visualizzazione più fluida, TVSDK a volte archivia il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.

TVSDK definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo iniziale del buffer entro il quale, prima dell’avvio della riproduzione del contenuto multimediale, deve essere di almeno 5 secondi. Dopo le chiamate dell’applicazione `play` ma prima dell’inizio della riproduzione, TVSDK memorizza in buffer il contenuto multimediale fino al momento iniziale per dare un inizio fluido quando inizia effettivamente la riproduzione.

È possibile modificare i tempi del buffer definendo nuovi criteri di buffering.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

A seconda dell’ambiente in uso (compreso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare criteri di buffering diversi per il lettore, ad esempio per modificare la durata minima del buffering iniziale e per la riproduzione in corso.

Dopo aver chiamato `play`, il lettore multimediale inizia a memorizzare il video nel buffering. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l’intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo aver inserito nel buffer i pochi secondi iniziali, inizia la riproduzione.

Durante il rendering del video, TVSDK continua a memorizzare nel buffer nuovi frammenti fino a quando non viene inserito nel buffer la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza del buffer corrente scende al di sotto del tempo del buffer di riproduzione, il lettore scarica altri frammenti. Quando la lunghezza del buffer corrente supera di alcuni secondi il tempo del buffer di riproduzione, TVSDK interrompe il download dei frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è alto, potrebbe assegnare all’utente un tempo di buffering iniziale lungo prima di iniziare. Questo potrebbe garantire una riproduzione fluida per un periodo di tempo più lungo; tuttavia, se le condizioni di rete sono scarse, la riproduzione iniziale potrebbe subire ritardi.
