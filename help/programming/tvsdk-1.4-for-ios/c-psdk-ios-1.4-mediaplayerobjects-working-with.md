---
description: L'oggetto PTMediaPlayer rappresenta il lettore multimediale. Un PTMediaPlayerItem rappresenta l'audio o il video sul lettore.
seo-description: L'oggetto PTMediaPlayer rappresenta il lettore multimediale. Un PTMediaPlayerItem rappresenta l'audio o il video sul lettore.
seo-title: Operazioni con gli oggetti MediaPlayer
title: Operazioni con gli oggetti MediaPlayer
uuid: eba26ad7-8c9a-4703-af32-1dfb928f6b67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Operazioni con gli oggetti MediaPlayer{#work-with-mediaplayer-objects}

L&#39;oggetto PTMediaPlayer rappresenta il lettore multimediale. Un PTMediaPlayerItem rappresenta l&#39;audio o il video sul lettore.

## Informazioni sulla classe MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Dopo che una risorsa multimediale è stata caricata correttamente, TVSDK crea un&#39;istanza della `PTMediaPlayerItem` classe per fornire l&#39;accesso a tale risorsa.

Consente di `PTMediaPlayer` risolvere la risorsa multimediale, caricare il file manifesto associato e analizzare il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L’ `PTMediaPlayerItem` istanza viene prodotta dopo che la risorsa è stata risolta e questa è una versione risolta di una risorsa multimediale. TVSDK consente di accedere all’ `PTMediaPlayerItem` istanza appena creata tramite `PTMediaPlayer.currentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all&#39;elemento del lettore multimediale.

## ciclo di vita dell’oggetto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

Dal momento in cui create l’ `PTMediaPlayer` istanza al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni da uno stato all’altro.

Alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, la chiamata `play` in `PTMediaPlayerStatusCreated` non è consentita. È possibile richiamare questo stato solo dopo che il lettore ha raggiunto lo `PTMediaPlayerStatusReady` stato.

Per utilizzare gli stati:

* È possibile recuperare lo stato corrente dell&#39;oggetto MediaPlayer con `PTMediaPlayer.status`.
* L&#39;elenco degli stati è definito in `PTMediaPlayerStatus`.

Diagramma di transizione dello stato per il ciclo di vita di un’istanza di MediaPlayer:
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
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreate</span> </p> </td> 
   <td colname="col2"> <p>L’applicazione ha richiesto un nuovo lettore multimediale chiamando <span class="codeph"> playerWithMediaPlayerItem</span>. Il nuovo lettore creato è in attesa di specificare un elemento del lettore multimediale. Questo è lo stato iniziale del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>L’applicazione chiama <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>e il lettore multimediale è in fase di caricamento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK ha impostato correttamente l'elemento del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>Il contenuto è preparato e gli annunci sono stati inseriti nella timeline, oppure la procedura di annuncio non è riuscita. È possibile avviare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlay</span> </p> </td> 
   <td colname="col2"> <p>L’applicazione ha chiamato <span class="codeph"> play</span>, pertanto TVSDK sta tentando di riprodurre il video. Prima della riproduzione del video potrebbe verificarsi un buffering. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>Durante la riproduzione e la pausa dell’applicazione, il lettore multimediale si sposta tra questo stato e <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è interrotta. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>L'applicazione ha rilasciato il lettore multimediale, che rilascia anche tutte le risorse associate. Non è più possibile utilizzare questa istanza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Errore durante il processo. Un errore potrebbe inoltre influire sulle operazioni che l'applicazione potrà eseguire successivamente. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Potete utilizzare lo stato per fornire un feedback sul processo (ad esempio, una casella di selezione in attesa della successiva modifica dello stato) o per eseguire il passaggio successivo nella riproduzione del supporto, ad esempio in attesa dello stato appropriato prima di chiamare il metodo successivo.

