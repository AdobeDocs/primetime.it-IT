---
description: Dal momento in cui crei l'istanza MediaPlayer al momento in cui la richiedi (riutilizzi o rimuovi), questa istanza completa una serie di transizioni tra stati.
title: Ciclo di vita dell'oggetto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Ciclo di vita dell&#39;oggetto MediaPlayer{#mediaplayer-object-lifecycle}

Dal momento in cui crei l&#39;istanza MediaPlayer al momento in cui la richiedi (riutilizzi o rimuovi), questa istanza completa una serie di transizioni tra stati.

Alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, non è consentito chiamare `play` in IDLE. Puoi chiamare questo stato solo dopo che il lettore ha raggiunto lo stato PREPARATO.

Per utilizzare gli stati:

* È possibile recuperare lo stato corrente dell&#39;oggetto `MediaPlayer` utilizzando la proprietà `MediaPlayer.status` .

   ```
   function get status():String;
   ```

* L’elenco degli stati è definito in `MediaPlayer.PlayerStatus`.

Diagramma di transizione dello stato per il ciclo di vita di un&#39;istanza `MediaPlayer`:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

La tabella seguente fornisce ulteriori dettagli:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus  </span> </th> 
   <th colname="col2" class="entry"> Si verifica quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INATTIVO  </span> </td> 
   <td colname="col2"> <p> L'applicazione ha richiesto un nuovo lettore multimediale creando un'istanza di <span class="codeph"> MediaPlayer </span>. Il lettore appena creato è in attesa di specificare un elemento del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INIZIALIZZAZIONE  </span> </td> 
   <td colname="col2"> <p>L'applicazione ha chiamato <span class="codeph"> MediaPlayer.replaceCurrentResource </span> e il lettore multimediale è in fase di caricamento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INIZIALIZZATO  </span> </td> 
   <td colname="col2"> <p>TVSDK: impostazione dell'elemento del lettore multimediale completata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARAZIONE  </span> </td> 
   <td colname="col2"> <p>L'applicazione ha chiamato <span class="codeph"> MediaPlayer.PrepareToPlay </span>. Il lettore multimediale sta caricando l'elemento del lettore multimediale e le risorse associate. </p> <p>Suggerimento:  Potrebbe verificarsi un buffering del supporto principale. </p> <p>TVSDK sta preparando il flusso multimediale e sta tentando di eseguire la risoluzione degli annunci e l'inserimento di annunci (se abilitato). </p> <p>Suggerimento:  Per impostare l'ora di inizio su un valore diverso da zero, chiama <span class="codeph"> PrepareToPlay(startTime) </span> con l'ora in millisecondi. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARATO  </span> </td> 
   <td colname="col2"> <p>Il contenuto è preparato e gli annunci sono stati inseriti nella timeline oppure la procedura dell’annuncio non è riuscita. È possibile iniziare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> GIOCO  </span> </td> 
   <td colname="col2"> <p>L'applicazione ha chiamato <span class="codeph"> play </span>, quindi TVSDK sta tentando di riprodurre il video. Potrebbe verificarsi un buffering prima che il video venga effettivamente riprodotto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IN PAUSA  </span> </td> 
   <td colname="col2"> <p>Quando l'applicazione riproduce e mette in pausa il contenuto multimediale, il lettore multimediale passa da questo stato a PLAYING. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RICERCA  </span> </td> 
   <td colname="col2"> <p>Il lettore multimediale cerca la posizione corretta durante la pausa o la riproduzione. Per determinare quando la ricerca è iniziata o terminata, ascolta gli eventi <span class="codeph"> SeekEvent.SEEK_BEGIN </span> e <span class="codeph"> SeekEvent.SEEK_END </span> . </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETATO  </span> </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è arrestata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RILASCIATO  </span> </td> 
   <td colname="col2"> <p>L'applicazione ha rilasciato il lettore multimediale, che rilascia anche le risorse associate. Non puoi più utilizzare questa istanza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRORE  </span> </td> 
   <td colname="col2"> <p>Errore durante il processo. Un errore potrebbe influire anche sulle operazioni che l'applicazione può eseguire in seguito. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>È possibile utilizzare lo stato per fornire un feedback sul processo (ad esempio, un&#39;icona che ruota in attesa della successiva modifica dello stato) o per effettuare il passaggio successivo durante la riproduzione del supporto, ad esempio per attendere lo stato appropriato prima di chiamare il metodo successivo.

