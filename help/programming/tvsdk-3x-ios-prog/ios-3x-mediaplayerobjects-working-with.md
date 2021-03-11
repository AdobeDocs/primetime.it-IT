---
description: L'oggetto PTMediaPlayer rappresenta il lettore multimediale. Un PTMediaPlayerItem rappresenta audio o video sul lettore.
title: Utilizzare gli oggetti MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Utilizzare gli oggetti MediaPlayer {#work-with-mediaplayer-objects}

L&#39;oggetto PTMediaPlayer rappresenta il lettore multimediale. Un PTMediaPlayerItem rappresenta audio o video sul lettore.

## Informazioni sulla classe MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Una volta caricata correttamente una risorsa multimediale, TVSDK crea un&#39;istanza della classe `PTMediaPlayerItem` per fornire l&#39;accesso a tale risorsa.

Il `PTMediaPlayer` risolve la risorsa multimediale, carica il file manifesto associato e analizza il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L’istanza `PTMediaPlayerItem` viene prodotta dopo la risoluzione della risorsa e questa istanza è una versione risolta di una risorsa multimediale. TVSDK fornisce l&#39;accesso all&#39;istanza `PTMediaPlayerItem` appena creata tramite `PTMediaPlayer.currentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all’elemento del lettore multimediale.

## Ciclo di vita dell&#39;oggetto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

Dal momento in cui crei l’istanza `PTMediaPlayer` al momento in cui la richiedi (riutilizzi o rimuovi), questa istanza completa una serie di transizioni da uno stato all’altro.

Alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, la chiamata a `play` in `PTMediaPlayerStatusCreated` non è consentita. Puoi chiamare questo stato solo dopo che il lettore ha raggiunto lo stato `PTMediaPlayerStatusReady` .

Per utilizzare gli stati:

* È possibile recuperare lo stato corrente dell&#39;oggetto MediaPlayer con `PTMediaPlayer.status`.
* L’elenco degli stati è definito in `PTMediaPlayerStatus`.

Diagramma di transizione dello stato per il ciclo di vita di un&#39;istanza MediaPlayer:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

La tabella seguente fornisce ulteriori dettagli:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>Si verifica quando</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione ha richiesto un nuovo lettore multimediale chiamando <span class="codeph"> playerWithMediaPlayerItem</span>. Il lettore appena creato è in attesa di specificare un elemento del lettore multimediale. Questo è lo stato iniziale del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInizializzazione</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione chiama <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span> e il lettore multimediale è in fase di caricamento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK: impostazione dell'elemento del lettore multimediale completata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>Il contenuto è preparato e gli annunci sono stati inseriti nella timeline oppure la procedura dell’annuncio non è riuscita. È possibile iniziare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlay</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione ha chiamato <span class="codeph"> play</span>, quindi TVSDK sta tentando di riprodurre il video. Potrebbe verificarsi un buffering prima che il video venga effettivamente riprodotto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>Quando l'applicazione riproduce e mette in pausa il contenuto multimediale, il lettore multimediale passa da questo stato a <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è arrestata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione ha rilasciato il lettore multimediale, che rilascia anche le risorse associate. Non puoi più utilizzare questa istanza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Errore durante il processo. Un errore potrebbe influire anche sulle operazioni che l'applicazione può eseguire in seguito. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>È possibile utilizzare lo stato per fornire un feedback sul processo (ad esempio, un&#39;icona che ruota in attesa della successiva modifica dello stato) o per effettuare il passaggio successivo durante la riproduzione del supporto, ad esempio per attendere lo stato appropriato prima di chiamare il metodo successivo.