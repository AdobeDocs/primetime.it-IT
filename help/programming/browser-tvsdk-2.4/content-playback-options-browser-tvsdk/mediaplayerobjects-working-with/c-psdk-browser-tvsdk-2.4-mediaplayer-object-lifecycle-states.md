---
description: Dal momento in cui l'istanza MediaPlayer viene creata al momento in cui viene terminata, questa istanza passa da uno stato all'altro.
title: Ciclo di vita e stati dell’oggetto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Ciclo di vita e stati dell&#39;oggetto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

Dal momento in cui l&#39;istanza MediaPlayer viene creata al momento in cui viene terminata, questa istanza passa da uno stato all&#39;altro.

Di seguito sono riportati gli stati possibili:

* **IDLE**:  `MediaPlayerStatus.IDLE`

* **INIZIALIZZAZIONE**:  `MediaPlayerStatus.INITIALIZING`

* **INIZIALIZZATO**:  `MediaPlayerStatus.INITIALIZED`

* **PREPARAZIONE**:  `MediaPlayerStatus.PREPARING`

* **PREPARATO**:  `MediaPlayerStatus.PREPARED`

* **RIPRODUZIONE**:  `MediaPlayerStatus.PLAYING`

* **IN PAUSA**:  `MediaPlayerStatus.PAUSED`

* **RICERCA**:  `MediaPlayerStatus.SEEKING`

* **COMPLETO**:  `MediaPlayerStatus.COMPLETE`

* **ERRORE**:  `MediaPlayerStatus.ERROR`

* **RILASCIATO**:  `MediaPlayerStatus.RELEASED`

L’elenco completo degli stati è definito in `MediaPlayerStatus`.

La conoscenza dello stato del lettore è utile perché alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, non è possibile chiamare `play` mentre si trova nello stato IDLE. Deve essere chiamato dopo aver raggiunto lo stato PREPARATO. Lo stato ERROR cambia anche ciò che può accadere in seguito.

Quando una risorsa multimediale viene caricata e riprodotta, il lettore effettua le transizioni nel modo seguente:

1. Lo stato iniziale è IDLE.
1. L&#39;applicazione chiama `MediaPlayer.replaceCurrentResource`, che sposta il lettore allo stato INITIALIZING.
1. Se il browser TVSDK carica correttamente la risorsa, lo stato diventa INITIALIZED.
1. L&#39;applicazione chiama `MediaPlayer.prepareToPlay` e lo stato cambia in PREPARAZIONE.
1. Il browser TVSDK prepara il flusso multimediale e avvia la risoluzione degli annunci e l&#39;inserimento degli annunci (se abilitato).

   Al termine di questo passaggio, gli annunci vengono inseriti nella timeline o la procedura dell’annuncio non è riuscita e lo stato del lettore diventa PREPARATO.
1. Quando l&#39;applicazione riproduce e mette in pausa il contenuto multimediale, lo stato si sposta tra PLAYING e PAUSED.

   >[!TIP]
   >
   >Durante la riproduzione o la pausa, quando si esce dalla riproduzione, si arresta il dispositivo o si passa alle applicazioni, lo stato cambia in SOSPESO e le risorse vengono rilasciate. Per continuare, ripristinare il lettore multimediale.

1. Quando il lettore raggiunge la fine del flusso, lo stato diventa COMPLETO.
1. Quando l&#39;applicazione rilascia il lettore multimediale, lo stato diventa RELEASED.
1. Se si verifica un errore durante il processo, lo stato diventa ERROR.

Ecco un&#39;illustrazione del ciclo di vita di un&#39;istanza MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

È possibile utilizzare lo stato per fornire all’utente un feedback sul processo (ad esempio, un’icona che ruota in attesa della modifica dello stato successivo) o per eseguire i passaggi successivi durante la riproduzione del contenuto multimediale, ad esempio l’attesa dello stato appropriato prima di chiamare il metodo successivo.

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

