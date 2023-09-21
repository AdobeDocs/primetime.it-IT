---
description: L'oggetto PTMediaPlayer rappresenta il lettore multimediale. PTMediaPlayerItem rappresenta audio o video sul lettore.
title: Utilizzare gli oggetti MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Utilizzare gli oggetti MediaPlayer{#work-with-mediaplayer-objects}

L&#39;oggetto PTMediaPlayer rappresenta il lettore multimediale. PTMediaPlayerItem rappresenta audio o video sul lettore.

## Informazioni sulla classe MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Una volta caricata correttamente una risorsa multimediale, TVSDK crea un’istanza di `PTMediaPlayerItem` per fornire accesso a tale risorsa.

Il `PTMediaPlayer` risolve la risorsa multimediale, carica il file manifesto associato e analizza il manifesto. Parte asincrona del processo di caricamento delle risorse. Il `PTMediaPlayerItem` l’istanza viene prodotta dopo che la risorsa è stata risolta e questa istanza è una versione risolta di una risorsa multimediale. TVSDK consente di accedere ai nuovi `PTMediaPlayerItem` istanza tramite `PTMediaPlayer.currentItem`.

>[!TIP]
>
>Prima di accedere all’elemento del lettore multimediale, devi attendere che la risorsa sia stata caricata correttamente.

## Ciclo di vita dell&#39;oggetto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

Dal momento in cui crei il `PTMediaPlayer` al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni da uno stato all&#39;altro.

Alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, chiamando `play` in `PTMediaPlayerStatusCreated` non è consentito. Puoi chiamare questo stato solo dopo che il lettore ha raggiunto `PTMediaPlayerStatusReady` stato.

Per utilizzare gli stati:

* È possibile recuperare lo stato corrente dell&#39;oggetto MediaPlayer con `PTMediaPlayer.status`.
* L’elenco degli stati è definito in `PTMediaPlayerStatus`.

Diagramma di transizione dello stato per il ciclo di vita di un’istanza MediaPlayer:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

La tabella seguente fornisce ulteriori dettagli:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> PTMediaPlayerStatus </th> 
   <th colname="col2" class="entry"> Si verifica quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione ha richiesto un nuovo lettore multimediale chiamando <span class="codeph"> playerWithMediaPlayerItem</span>. Il lettore appena creato è in attesa di specificare un elemento del lettore multimediale. Stato iniziale del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>Chiamate dell'applicazione <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>e il lettore multimediale è in fase di caricamento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK: impostazione dell'elemento del lettore multimediale completata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>Il contenuto viene preparato e gli annunci sono stati inseriti nella timeline, oppure la procedura dell’annuncio non è riuscita. Può iniziare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione ha chiamato <span class="codeph"> play</span>, quindi TVSDK sta tentando di riprodurre il video. Alcuni buffering potrebbero verificarsi prima dell’effettiva riproduzione del video. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>Quando l’applicazione riproduce e mette in pausa il contenuto multimediale, il lettore multimediale si sposta tra questo stato e <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è interrotta. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>L’applicazione ha rilasciato il lettore multimediale, con tutte le risorse associate. Non è più possibile utilizzare questa istanza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Si è verificato un errore durante il processo. Un errore può inoltre influire sulle operazioni successive dell'applicazione. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>È possibile utilizzare lo stato per fornire un feedback sul processo (ad esempio, uno spinner in attesa della modifica di stato successiva) o per fare il passaggio successivo nella riproduzione del supporto, ad esempio attendere lo stato appropriato prima di chiamare il metodo successivo.
