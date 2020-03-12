---
description: Dal momento in cui l’istanza MediaPlayer viene creata al momento in cui viene terminata, questa passa da uno stato all’altro.
seo-description: Dal momento in cui l’istanza MediaPlayer viene creata al momento in cui viene terminata, questa passa da uno stato all’altro.
seo-title: Ciclo di vita e stati dell'oggetto MediaPlayer
title: Ciclo di vita e stati dell'oggetto MediaPlayer
uuid: fe76ea80-aaa8-43bc-9b81-85e0551f70dd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Ciclo di vita e stati dell&#39;oggetto MediaPlayer{#life-cycle-and-states-of-the-mediaplayer-object}

Dal momento in cui l’istanza MediaPlayer viene creata al momento in cui viene terminata, questa passa da uno stato all’altro.

Gli stati possibili sono i seguenti:

* **IDLE**: `MediaPlayerStatus.IDLE`

* **INIZIALIZZAZIONE**: `MediaPlayerStatus.INITIALIZING`

* **INIZIALIZZATO**: `MediaPlayerStatus.INITIALIZED`

* **PREPARAZIONE**: `MediaPlayerStatus.PREPARING`

* **PREPARATO**: `MediaPlayerStatus.PREPARED`

* **RIPRODUZIONE**: `MediaPlayerStatus.PLAYING`

* **PAUSA**: `MediaPlayerStatus.PAUSED`

* **RICERCA**: `MediaPlayerStatus.SEEKING`

* **COMPLETO**: `MediaPlayerStatus.COMPLETE`

* **ERRORE**: `MediaPlayerStatus.ERROR`

* **RILASCIATO**: `MediaPlayerStatus.RELEASED`

L’elenco completo degli stati è definito in `MediaPlayerStatus`.

È utile conoscere lo stato del lettore perché alcune operazioni sono consentite solo mentre il lettore si trova in uno stato particolare. Ad esempio, `play` non può essere chiamato mentre si trova nello stato IDLE. Deve essere chiamato dopo aver raggiunto lo stato PREPARATO. Lo stato ERROR modifica anche ciò che può accadere in seguito.

Quando una risorsa multimediale viene caricata e riprodotta, il lettore passa come segue:

1. Lo stato iniziale è IDLE.
1. Le chiamate dell&#39;applicazione `MediaPlayer.replaceCurrentResource`, che sposta il lettore allo stato INITIALIZING.
1. Se l&#39;SDK del browser carica correttamente la risorsa, lo stato è INITIALIZED.
1. Le chiamate dell&#39;applicazione `MediaPlayer.prepareToPlay`e lo stato diventa PREPARAZIONE.
1. Browser TVSDK prepara il flusso multimediale e avvia la risoluzione degli annunci e l&#39;inserimento degli annunci (se attivato).

   Quando questo passaggio è completo, gli annunci vengono inseriti nella timeline o la procedura di annuncio non è riuscita e lo stato del lettore cambia in PREPARATO.
1. Durante la riproduzione e la pausa dell’applicazione, lo stato si sposta tra PLAYING e PAUSED.

   >[!TIP]
   >
   >Durante la riproduzione o la pausa, quando si esce dalla riproduzione, si arresta il dispositivo o si passa alle applicazioni, lo stato cambia in SOSPESO e le risorse vengono rilasciate. Per continuare, ripristinare il lettore multimediale.

1. Quando il lettore raggiunge la fine del flusso, lo stato diventa COMPLETE.
1. Quando l’applicazione rilascia il lettore multimediale, lo stato diventa RELEASED.
1. Se si verifica un errore durante il processo, lo stato diventa ERRORE.

Di seguito è riportata un&#39;illustrazione del ciclo di vita di un&#39;istanza di MediaPlayer:

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

Potete utilizzare lo stato per fornire un feedback all’utente sul processo (ad esempio, una casella di selezione in attesa della successiva modifica dello stato) o per effettuare i passaggi successivi durante la riproduzione del supporto, ad esempio l’attesa dello stato appropriato prima di chiamare il metodo successivo.

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

