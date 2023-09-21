---
description: Dal momento in cui viene creata l'istanza MediaPlayer al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni tra gli stati.
title: Ciclo di vita dell'oggetto MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Ciclo di vita dell&#39;oggetto MediaPlayer{#mediaplayer-object-lifecycle}

Dal momento in cui viene creata l&#39;istanza MediaPlayer al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni tra gli stati.

Alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, chiamando `play` in `IDLE` non è consentito. Puoi chiamare questo stato solo dopo che il lettore ha raggiunto `PREPARED` stato.

Per utilizzare gli stati:

* È possibile recuperare lo stato corrente del `MediaPlayer` oggetto con `MediaPlayer.getStatus`.

  ```java
  PlayerState getStatus() throws IllegalStateException;
  ```

* L’elenco degli stati è definito in `MediaPlayer.PlayerState`.

Diagramma di transizione dello stato per il ciclo di vita di una `MediaPlayer` istanza:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

La tabella seguente fornisce ulteriori dettagli:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Si verifica quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INATTIVO </span> </td> 
   <td colname="col2"> <p>L'applicazione ha richiesto un nuovo lettore multimediale chiamando <span class="codeph"> DefaultMediaPlayer.create </span>. Il lettore appena creato è in attesa di specificare un elemento del lettore multimediale. Questo è lo stato iniziale del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INIZIALIZZAZIONE </span> </td> 
   <td colname="col2"> <p>Chiamata dell'applicazione <span class="codeph"> MediaPlayer.replaceCurrentItem </span>e il lettore multimediale è in fase di caricamento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INIZIALIZZATO </span> </td> 
   <td colname="col2"> <p>TVSDK: impostazione dell'elemento del lettore multimediale completata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARAZIONE </span> </td> 
   <td colname="col2"> <p>Chiamata dell'applicazione <span class="codeph"> MediaPlayer.preparationToPlay </span>. Il lettore multimediale sta caricando l’elemento del lettore multimediale e le risorse associate. </p> <p>Suggerimento: potrebbe verificarsi un buffering del file multimediale principale. </p> <p>TVSDK sta preparando il flusso multimediale e sta tentando di eseguire la risoluzione e l’inserimento degli annunci (se abilitati). </p> <p>Suggerimento: per impostare un valore diverso da zero come ora di inizio, invoca <span class="codeph"> preparationToPlay(startTime) </span> con il tempo in millisecondi. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARATO </span> </td> 
   <td colname="col2"> <p>Il contenuto viene preparato e gli annunci sono stati inseriti nella timeline, oppure la procedura dell’annuncio non è riuscita. Può iniziare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RIPRODUZIONE </span> </td> 
   <td colname="col2"> <p>L'applicazione ha chiamato <span class="codeph"> play </span>, quindi TVSDK sta tentando di riprodurre il video. Alcuni buffering potrebbero verificarsi prima dell’effettiva riproduzione del video. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IN PAUSA </span> </td> 
   <td colname="col2"> <p>Quando l’applicazione riproduce e mette in pausa il contenuto multimediale, il lettore multimediale si sposta tra questo stato e PLAY. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SOSPESO </span> </td> 
   <td colname="col2"> <p>L’applicazione si è allontanata dalla riproduzione, ha spento il dispositivo o ha cambiato applicazione durante la riproduzione o la pausa del lettore. Il lettore multimediale è stato sospeso e le risorse sono state rilasciate. Per continuare, ripristina il lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETATO </span> </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è interrotta. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RILASCIATO </span> </td> 
   <td colname="col2"> <p>L’applicazione ha rilasciato il lettore multimediale, con tutte le risorse associate. Non è più possibile utilizzare questa istanza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRORE </span> </td> 
   <td colname="col2"> <p>Si è verificato un errore durante il processo. Un errore può inoltre influire sulle operazioni successive dell'applicazione. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>È possibile utilizzare lo stato per fornire un feedback sul processo (ad esempio, uno spinner in attesa della modifica dello stato successiva) o per eseguire il passaggio successivo nella riproduzione del file multimediale, ad esempio l&#39;attesa dello stato appropriato prima di chiamare il metodo successivo.

Ad esempio:

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```
