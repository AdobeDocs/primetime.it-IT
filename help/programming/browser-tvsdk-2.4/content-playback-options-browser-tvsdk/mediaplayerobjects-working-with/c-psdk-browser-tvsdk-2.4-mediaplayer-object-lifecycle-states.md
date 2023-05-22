---
description: Dal momento in cui viene creata l’istanza MediaPlayer al momento in cui viene terminata, questa istanza passa da uno stato all’altro.
title: Ciclo di vita e stati dell'oggetto MediaPlayer
exl-id: 26cad982-ef85-42fb-aaa7-e5d494088766
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Ciclo di vita e stati dell&#39;oggetto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

Dal momento in cui viene creata l’istanza MediaPlayer al momento in cui viene terminata, questa istanza passa da uno stato all’altro.

Di seguito sono riportati gli stati possibili:

* **INATTIVO**: `MediaPlayerStatus.IDLE`

* **INIZIALIZZAZIONE**: `MediaPlayerStatus.INITIALIZING`

* **INIZIALIZZATO**: `MediaPlayerStatus.INITIALIZED`

* **PREPARAZIONE**: `MediaPlayerStatus.PREPARING`

* **PREPARATO**: `MediaPlayerStatus.PREPARED`

* **RIPRODUZIONE**: `MediaPlayerStatus.PLAYING`

* **IN PAUSA**: `MediaPlayerStatus.PAUSED`

* **RICERCA**: `MediaPlayerStatus.SEEKING`

* **COMPLETATO**: `MediaPlayerStatus.COMPLETE`

* **ERRORE**: `MediaPlayerStatus.ERROR`

* **RILASCIATO**: `MediaPlayerStatus.RELEASED`

L&#39;elenco completo degli stati è definito in `MediaPlayerStatus`.

Conoscere lo stato del lettore è utile perché alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio: `play` non può essere chiamato mentre si trova nello stato IDLE. Deve essere richiamato dopo aver raggiunto lo stato PREPARATO. Lo stato ERROR cambia anche in ciò che può accadere successivamente.

Quando una risorsa multimediale viene caricata e riprodotta, il lettore passa nel modo seguente:

1. Lo stato iniziale è IDLE.
1. Chiamate dell&#39;applicazione `MediaPlayer.replaceCurrentResource`, che porta il lettore allo stato INITIALIZING.
1. Se il TVSDK del browser carica correttamente la risorsa, lo stato diventa INIZIALIZZATO.
1. Chiamate dell&#39;applicazione `MediaPlayer.prepareToPlay`e lo stato cambia in PREPARAZIONE.
1. Il browser TVSDK prepara il flusso multimediale e avvia la risoluzione e l’inserimento dell’annuncio (se abilitati).

   Al termine di questo passaggio, gli annunci vengono inseriti nella timeline o la procedura pubblicitaria non è riuscita e lo stato del lettore cambia in PREPARATO.
1. Quando l&#39;applicazione riproduce e mette in pausa il contenuto multimediale, lo stato si sposta tra PLAY e PAUSED.

   >[!TIP]
   >
   >Durante la riproduzione o la pausa, quando ci si allontana dalla riproduzione, si arresta il dispositivo o si cambia applicazione, lo stato cambia in SOSPESO e le risorse vengono rilasciate. Per continuare, ripristina il lettore multimediale.

1. Quando il lettore raggiunge la fine del flusso, lo stato diventa COMPLETE.
1. Quando l’applicazione rilascia il lettore multimediale, lo stato cambia in RILASCIATO.
1. Se si verifica un errore durante il processo, lo stato cambia in ERRORE.

Ecco un&#39;illustrazione del ciclo di vita di un&#39;istanza MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

È possibile utilizzare lo stato per fornire all&#39;utente un feedback sul processo (ad esempio, un girante in attesa della modifica dello stato successivo) o per eseguire i passaggi successivi nella riproduzione del contenuto multimediale, ad esempio l&#39;attesa dello stato appropriato prima di chiamare il metodo successivo.

Ad esempio:

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```
